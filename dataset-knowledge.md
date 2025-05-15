---
icon: book-atlas
---

# Dataset Knowledge

### I. Common Classifications of Fine-tuning Datasets

Many people are confused about what format the data fed to the model should be in, which is actually because they haven't distinguished several common types of fine-tuning tasks. In order to solve different problems in different business scenarios, the types of fine-tuning tasks we may adopt are different, so the dataset formats used will also differ. Therefore, to clarify what kind of dataset format we need to organize, we first need to understand what kind of task scenario our fine-tuning belongs to. Below is a classification diagram of common fine-tuning tasks that I have sorted out:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=YmQzNjNhMWFmOWRhODg5M2UzZmQzODFjZDE4NGQ2MmZfWFFsTFM0VG9IMW93cFZMZ3ljZmVmVzhWSU5MbmYwZW5fVG9rZW46UVM3eWJoZERjb25hUFZ4WXg3NWNTWnZRbmZoXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

#### 1.1 Pre-training

Training a model from scratch is generally called pre-training. The purpose of this process is to enable the model to master the general rules of language and basic language understanding capabilities. Currently, mainstream large models in the market, such as `ChatGPT, DeepDeek`, etc., are all "autoregressive models", and the essence of "autoregressive models" is:

* **Using past self to predict future self**.

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=YWI4OGY3ODBlODFiYzhlZjM1YmU0N2VmOGZkNzVhZTBfeTRaT3dIWm1Db2Ftakp1OElpdmxUdUtwd3VROVF5SGNfVG9rZW46R0tFemJNa0p4b1FWMDR4NHJ4V2NCZkRUbktjXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

We all know that when large models output text, they output according to `Token`. `Token` can be simply understood as breaking sentences into minimal semantic units (such as Chinese characters/words, English words or subwords). The answer is divided into 4 `Tokens`, each `Token` is predicted based on the previous question + already output `Tokens`. The more frequently these keywords appear together in the pre-training dataset, the greater the probability the model will output them. So the richer our dataset, the higher the accuracy of the model's prediction of `Token` output, and the better the final output effect. Therefore, in the pre-training process, we generally use massive unstructured text (such as books, web pages, conversations) to train the model by "predicting the next word", which means that there are no explicit requirements for the format of the pre-training dataset. For example, the following data can be used directly for training: But for fine-tuning in specific domains, unstructured text cannot be used. We can understand it this way:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=MTkzNzY3MmY0OWM4OWIxYzc4OWI4MGEyODhkNmQ5ZjFfampweXpadWVFUWxKSW80ZFhoOXpHSFZacUFyc3NjaG9fVG9rZW46QXg1TmJvblJjb0pTdHN4UW02b2N2VEx3bkpjXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

* **Pre-training stage**: Like a baby learning to speak, hearing various sounds (unstructured), regardless of what they are, just let them listen more, and gradually they will learn the rules of language;
* **Instruction fine-tuning stage**: Like teaching a child what to do "when hearing a question, answer it", you need to clearly tell them what the question is and what the correct answer is. If you continue to use irregular (unstructured) conversation, they won't have a deep impression of what you want them to learn.

And the pre-training process can be understood as a process of learning and developing abilities without human supervision. Correspondingly, if we want the model to have specific capabilities, supervised fine-tuning is needed.

***

#### 1.2 Supervised Fine-Tuning

Supervised Fine-Tuning (SFT), as the name suggests, requires human supervision during the fine-tuning process. For example: if we want to train an English-Chinese translation model, translating English to Chinese is a very clear demand scenario, so in the dataset, we only need to have input and output:

```json
{"input": "Hello", "output": "你好"}
```

**1.2.1 Instruction Fine-tuning**

What if we want the model to have the ability to understand multiple languages? In this case, two fields alone are not enough, because when the `Input` is the same word, according to the different tasks we want the model to complete, the `output` may be different. At this time, we need to introduce the concept of instruction, such as this dataset:

```json
[
  {
    "instruction": "Translate this English sentence into French",
    "input": "Hello, how are you?",
    "output": "Bonjour, comment ça va ?"
  },
  ...
]
```

We tell the model the clear instruction: translate English to French, and then tell the model the `Input` (English) and `Output` (French), so that the model can accurately understand what to do. This is instruction fine-tuning. Common business scenarios for instruction fine-tuning:

* **Intelligent Education**: Implement homework assistance, plan personalized learning paths, assist language learning.
* **Intelligent Office**: Can handle documents, emails, and schedule management.
* **Intelligent Translation**: Applied to professional field translation, specific scenario translation, and multilingual interaction.
* **Data Analysis**: Let the model provide accurate interpretation and insights of data according to analysis requirement instructions.

Typical open-source datasets for instruction fine-tuning (including instruction, input, output fields):

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2Q0MjVjZDQzODg5NjkxMzRiMDIwODAxMDg4MDIxYmNfWlVhZHRWRnlVTmhHeVpzYXhYNVk2UnFNbFB2dzRPNFFfVG9rZW46R2RITmI2a0dab2RQajB4VVBDN2NYMVJwblFlXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> `Alpaca` dataset: Created by Stanford University, generated through fine-tuning models, containing about 52,000 instruction following data samples. It covers various tasks, such as common sense Q&A, text generation, etc., helping models optimize in terms of instruction understanding and generation.

***

**1.2.2 Dialogue Fine-tuning**

Dialogue Fine-tuning (`Dialogue Tuning`) is to train models to generate coherent, contextual responses through multi-turn dialogue data, emphasizing the understanding of dialogue history context and the naturalness and fluency of responses. Its core is to teach the model to handle logical relationships, emotional expressions, and role identities in dialogues. Dialogue fine-tuning datasets typically include the context of the dialogue and the corresponding responses.

```javascript
[
  {
    "dialogue": [
      {"role": "user", "content": "今天天气怎么样？"},
      {"role": "assistant", "content": "北京今日多云转晴，气温22℃，适合户外活动。"},
      {"role": "user", "content": "那适合去长城吗？"},
      {"role": "assistant", "content": "长城景区海拔较高，建议携带外套，注意防晒。"}
    ]
  },
  ...
]
```

The core features of dialogue fine-tuning datasets: containing multi-turn dialogue context, annotated role identities, focusing on response coherence and logic. Through such data, the model can learn how to generate appropriate responses in different dialogue scenarios, thereby improving the coherence and relevance of dialogues. Common business scenarios for dialogue fine-tuning:

* **Intelligent Customer Service Systems**: Improve the dialogue ability of customer service robots in handling user inquiries, more accurately understanding user intentions and providing solutions.
* **Chatbots**: Make chatbots more naturally engage in multi-turn conversations with users, improving user experience.
* **Voice Assistants**: Optimize voice assistants' dialogue performance in voice interactions, making them more in line with user expectations.

Typical open-source datasets for dialogue fine-tuning:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmIxOTIyZDQ1MTg3ZTg5ZDFlODFmNTUzZDdhMTIxYzRfSVFZbHhqT2JKRjhkU3pidktrV1VkQlJqMmljM0JCazRfVG9rZW46TGFnV2JYdEV4b3ByRTZ4dVRXNmNYRGtSbjlmXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> A multilingual Q&A dataset for training dialogue models, with content structure and style conforming to the ShareGPT dialogue format. Each sample in the dataset is a dialogue turn, including human questions and model answers. The data covers multiple languages (English, Spanish, Chinese, Russian, etc.) and diverse domains.

***

**1.2.3 Domain Adaptation**

Domain Adaptation refers to fine-tuning models on data from specific domains to better adapt them to tasks and requirements in those specific domains.

```json
[
  {
    "instruction": "Analyze the patient's symptom description",
    "input": "55-year-old male, persistent retrosternal pain for 3 hours, nitroglycerin sublingual ineffective",
    "output": "Possible diagnosis: Acute myocardial infarction (STEMI), recommend immediate ECG examination and myocardial enzyme profile test",
    "domain": "Medical"
  },
  {
    "instruction": "Explain legal provisions",
    "input": "Article 1032 of the Civil Code",
    "output": "This provision stipulates that natural persons enjoy the right to privacy, and no organization or individual may infringe upon others' privacy rights by means of spying, harassment, disclosure, publication, etc.",
    "domain": "Legal"
  },
  ...
]
```

Core features of domain adaptation datasets: domain terminology annotation (such as medical ontology library, legal terminology library), complex rule modeling (such as drug interactions, contract clause logic), scenario-based data augmentation (such as simulated medical consultation dialogues, contract review processes); Typical business scenarios for domain adaptation:

* **Medical Domain Adaptation**: Used for medical record analysis, disease diagnosis assistance, medical literature retrieval, etc.
* **Legal Domain Adaptation**: Assist in legal document analysis, case retrieval, contract review, etc.
* **Financial Domain Adaptation**: Used for risk assessment, market analysis report generation, financial product recommendation, etc.

Typical open-source datasets for domain adaptation:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=ODQxNjI5NzIzYmU2ZWIyYjEzM2NmZWRhZmFmODQxMmNfOHdNQUJZaDcxZkhXOWpUNmJRNVVHOGFuWmdvZ0FwNUlfVG9rZW46SlV2aWJDWGNmb1JBakl4UVpZS2N0RmNhbk5GXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> A medical Q&A dataset based on `PubMed` literature, containing medical research-related questions, suitable for medical information extraction and domain adaptation tasks.

***

**1.2.4 Text Classification**

Text Classification is a classic task in natural language processing, with the purpose of training models to predict categories or assign labels to text through annotated data. This type of task requires the model to understand the relationship between text semantics and category features, and is suitable for scenarios that require structured output.

```json
[
  {"text": "This phone has a battery life of up to 48 hours, and the photo effect is amazing", "label": "positive"},
  {"text": "The system frequently stutters, and the customer service response is slow", "label": "negative"},
  {"text": "Quantum computers breakthrough in new error correction code technology", "label": "science_news"},
  {"text": "The central bank announced a 0.5 percentage point reduction in the reserve requirement ratio", "label": "finance_news"}
]
```

Typical business scenarios for text classification fine-tuning:

* **Sentiment Analysis**: Product review sentiment polarity recognition (positive/negative/neutral)
* **Content Moderation**: Detecting inappropriate content (political/violent/advertising)
* **News Classification**: Automatic categorization into finance/technology/sports sections
* **Intent Recognition**: User query classification (inquiry/complaint/price comparison)

Typical open-source datasets for text classification:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=NjAyNTM3MGVhYTg4NjAwMDlkMDMzOTNiNGM2N2FkZWRfYjU3WnNJN0NicUxZQkY1WDBrVlNOZmZsWlRzdG1WTTlfVG9rZW46V0NiZGI2Y21hb0VaY1Z4aFpDZ2MxVUJWbnJMXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> `imdb` Large Movie Review Dataset, containing the mapping relationship from user reviews to movie ratings, suitable for fine-tuning tasks to classify reviews as positive or negative.

***

**1.2.5 Model Reasoning Fine-tuning**

Fine-tuning reasoning models is actually a special form of supervised fine-tuning. By explicitly annotating the chain of thought (`Chain of Thought, COT`) in the dataset, the model is trained not only to provide the final answer but also to generate the logical reasoning process. The core lies in enabling the model to learn "step-by-step thinking", applicable to scenarios requiring complex logical reasoning (e.g., mathematical proofs, code debugging). In datasets used for reasoning model fine-tuning, it is usually necessary to additionally include the model's thought process:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=NjdhMzc0ZWJmOGVjN2YyNTA4NDJmZGRjNzllYmU0NzNfVFRKMVhJSFE5alE0NkJ1eEVFRktDTld5anhCTzdJN01fVG9rZW46UDJJNGJITDZSb1VRTmh4RndwdWNFMkVvbnFiXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

```json
[
  {
    "instruction": "Solve a math application problem",
    "input": "Xiao Ming bought 3 pencils, each costing 2 yuan; he also bought 5 notebooks, each costing 4 yuan more than a pencil. How much did he spend in total?",
    "chain_of_thought": [
      "Pencil price: 2 yuan/each → 3 pencils total price: 3×2=6 yuan",
      "Notebook price: 2+4=6 yuan/each → 5 notebooks total price: 5×6=30 yuan",
      "Total cost: 6+30=36 yuan"
    ],
    "output": "The total cost is 36 yuan"
  },
  ...
]
```

Note: Not all tasks are suitable for reasoning models, as reasoning models are prone to hallucinations. In some cases, using reasoning models may have counterproductive effects. When handling simple and straightforward tasks, reasoning models may overcomplicate problems, leading to overthinking, slower responses, and even increased hallucination risks. For example, if you ask a reasoning model to perform retrieval or explanation tasks, when it cannot find reference information, it will generate output based on its own reasoning process, which may not be accurate. The following are scenarios suitable for reasoning model fine-tuning:

* **Code Generation and Debugging**: Reasoning models can understand complex programming problems, generate efficient code solutions, and assist developers in code debugging.
* **Mathematical Problem Solving**: In mathematical modeling, complex calculations, and logical reasoning tasks, reasoning models excel at providing detailed problem-solving steps and accurate answers.
* **Complex Data Analysis**: Reasoning models are adept at handling complex data analysis tasks requiring multi-step reasoning and strategic planning, aiding scientists and researchers in deeper data mining.
* **Legal and Financial Analysis**: When processing complex documents like legal contracts and financial agreements, reasoning models can extract key clauses, interpret ambiguous information, and assist decision-making.
* The chain of thought in datasets may be relatively easy to obtain in specific scenarios. For example, in mathematical reasoning task fine-tuning, the problem-solving process inherently present in the dataset can serve as the chain of thought, such as in the following mathematical problem-solving dataset:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=M2VmYTM4MzI3YjU1ZDFmYWRiMWE3YmYwMWJmMjA5NzlfQmViakxzcHNCYW9xWjBmSlB2T1o0NUFYcWRiMU01cllfVG9rZW46UmFZemJENjBjb0VWQzF4eW9EM2N2TDBObkJkXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> Approximately 860,000 Chinese high school math practice problems, as well as problems from American and international math Olympiads, with each problem's solution presented in the chain of thought (CoT) format.

Another approach is through distillation from large models with reasoning capabilities, such as those derived from `DeepSeek-R1` and other reasoning models.

***

#### 1.3 Knowledge Distillation

Knowledge Distillation (`Knowledge Distillation`) is a technique that transfers knowledge from complex models (teacher models) to lightweight models (student models). By optimizing student models to produce outputs close to the teacher models' "soft labels", it reduces inference costs while maintaining performance. Constructing model distillation datasets should be the simplest scenario - when you fully trust the large model's outputs, you can directly use its generated Q&A pairs as the dataset, followed by manual quality assessment and validation. Typical open-source model distillation datasets:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDIyODM2MjQ0YWMwZDY5OWQyNDAwZjljYWUyZGE1ZjVfSFltaFliazNkSmFQWWFPZWZPTktKRzUwMWNQS3hobEZfVG9rZW46Slo1cWJwdWhWb2tTV3J4bjZUdWNQZDZmbm9lXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> Chinese dataset distilled from full-capability DeepSeek-R1, containing not only math data but also extensive general-purpose data, totaling 110K entries.

***

#### 1.4 Other Fine-tuning Techniques

**1.4.1 Reinforcement Learning Fine-tuning**

Reinforcement learning fine-tuning builds upon supervised fine-tuning by actively incorporating human feedback to optimize model generation quality. Its core lies in introducing reward models (`Reward Model`) to evaluate the rationality of generated results and adjusting model parameters through reinforcement learning strategies (e.g., `PPO` algorithm) to make outputs better align with human preferences.

```json
[
  {
    "input": "Recommend a science fiction movie",
    "output": "Interstellar is a classic science fiction film that explores time and family.",
    "reward_score": 4.5  // Human-annotated quality score (0-5)
  },
  {
    "input": "Explain black hole theory",
    "output": "Black holes are mysterious celestial bodies composed of dark matter, consuming all matter.",
    "reward_score": 2.0  // Contains incorrect information, low score
  }
]
```

Reinforcement learning fine-tuning is typically applied in the following business scenarios:

* **Dialogue System Optimization**: After supervised fine-tuning for relevance, further align the model with human values (safety, harmlessness, usefulness).
* **Content Generation**: After supervised fine-tuning for writing ability, further optimize output style (e.g., humor, formality) or avoid sensitive information.
* **Code Generation**: After supervised fine-tuning for code generation ability, further optimize code readability and correctness.

Typical open-source reinforcement learning datasets:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=MDI4MDEwNDMxNTA5ZmNhN2NlYWI5OTNjMTY0NWFlMGVfUkk1b05uOWVYUEY4UzdLUHF4RVdWRTBZczN6Zzdnb2hfVG9rZW46SDJEM2I3RFc3b2g2WVp4WUFEc2MwNVVxbjllXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> Human preference ranking dataset for reinforcement learning fine-tuning and training reward models.

***

**1.4.2 Multimodal Fine-tuning**

Multimodal fine-tuning (`Multimodal Fine-Tuning`) refers to training models with multiple modalities (text, images, audio, etc.) to enable cross-modal understanding and generation capabilities. This is a parallel category to text-based model fine-tuning, also encompassing supervised/unsupervised fine-tuning, reinforcement learning fine-tuning, and other categories.

```json
[
  {
    "text": "A cat is chasing a butterfly",
    "image_url": "https://example.com/cat.jpg",
    "caption": "An orange cat is chasing a white butterfly in the garden"
  },
  {
    "audio": "audio.wav",
    "text": "Transcription of meeting recording: Today's agenda is...",
    "summary": "The meeting discussed Q3 sales targets and market strategies"
  }
]
```

Note that the image, video, and audio data can be in the form of URLs, base64 encoding, or stored directly on Hugging Face. The key is that the data can be read during training.

Multimodal fine-tuning is typically applied in the following business scenarios:

* **Image-Text Question Answering**: Input images and questions, generate answers.
* **Video Content Understanding**: Analyze video frames and subtitles, generate summaries.
* **Cross-Modal Retrieval**: Search for relevant images/videos based on text descriptions.

Typical open-source multimodal fine-tuning datasets:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=MDdlYzkzZjU2MGQ0MTQyZmYyYWJjNmY5OWY2ZmY2NWJfUk8wRVhXRWt2elFTNGthMFNsZUhKUmpuNHM2V2E3S29fVG9rZW46Qmh1R2JUZThZb2U5bXN4UThTbWNPV1BzbllsXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

> A collection of 50 large-scale visual language training datasets (only training sets), used for multimodal vision-language model fine-tuning. The dataset structure includes `images` (image list) and `texts` (dialogue text), with dialogues presented in a user-question, model-answer format, covering tasks like TQA (Text-Image Question Answering).

***

### Two, Common Data Formats for Fine-tuning

There is no specific format requirement for model fine-tuning datasets. We generally eliminate differences in various fine-tuning dataset formats in the code. Let's review the code from the previous fine-tuning tutorial:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=NzRlNGQ2NDE1YzkzMDI1NzVkNTJmOTdmNGFlYWM3MDVfTERTazI0VlNuRlplb1lZanowSmNqSkNVMWxHdmpWTXNfVG9rZW46Wm0yZGJoTXR1b3BpR1J4bENWemNPTzlkbnF3XzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

This code defines a template for formatting fine-tuning datasets, where the three "{}" represent the three variables to be passed in, corresponding to the original problem, thought process, and final answer, respectively.

***

#### 2.1 Alpaca

`Alpaca` was initially released by Stanford University in 2023 as a **52k instruction fine-tuning dataset**, generated by `OpenAI`'s `text-davinci-003` model to optimize large language models (like `LLaMA`) through instruction following tasks. Later, with community development, Alpaca's JSON structure evolved into a **universal data format**, extending fields like `system` (system prompts) and `history` (conversation history), supporting multi-turn dialogue tasks. Suitable for various fine-tuning scenarios, many mainstream frameworks (like LLaMA-Factory, DeepSpeed) can directly load `Alpaca`-formatted datasets. Here, we reference two examples of `Alpaca`-formatted datasets in different fine-tuning scenarios from `LLaMA-Factory`:

**Alpaca format for instruction fine-tuning datasets**:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=MjgzNzVmM2NiNGQ3MDkyOGQ3OGFlMDk2M2NlYzcwNmFfUmIxQ25XdGozTkxsQjRDVTBla01wTWtvTTV3ZDVITEZfVG9rZW46VGxJTWJycGtQb041WXZ4dEUzQWNuYm5QbnlmXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

**Alpaca format for domain adaptation fine-tuning datasets**:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=M2ZmNzM3N2UwOGUyNGY5OWQ2MmVkZjM5YTI0ODAxNDZfN0NUdHB5RnViZXBoa1RyOWtyak12UG5SZ1d3V0xpRDdfVG9rZW46TWZDS2JWUTg5bzNiZ0d4NmVNWmN0MzFJbjFxXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

**Alpaca format for preference datasets**:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=NDJiMjNiMzkwOTg2NTYyY2U1ZmJjNmYwNmUyOTEyYTlfWXNaZ3AzMXZVdnFwR0k4MkZmUVljSUd6Yk45MmpmRXZfVG9rZW46QTdWM2JtNnlMb1lmRTd4QXdRb2NzUVRhbm5iXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

#### 2.2 ShareGPT

**ShareGPT** was originally a data format standard designed by the community to normalize model training data storage for multi-turn dialogue and tool invocation scenarios. Its core objective is to support complex interactions (e.g., user query → tool invocation → result integration) through structured fields like `conversations` lists and `tools` descriptions. As the format gained popularity, the community built several specific datasets based on the ShareGPT format, collectively known as "ShareGPT-format datasets".

**ShareGPT-format Instruction Fine-tuning Dataset**:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=NDZmNGJiZTA0MWY2NzcyOTgyZjQ4YWQ0MzQ4NDEzYmNfaTZEVm5lS0N5aTVpNXNRS2g0U3lyRmdpY2hvQ3B4bUtfVG9rZW46SDkzSmJzQXcwb3VEakF4T3RjSGNtTVdYbmFmXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

**ShareGPT-format Preference Dataset**:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDNkNDcwNTI1ODBhMzkyNGI4MDI1OWMxM2JhYTQ2ZDVfeDdlMVZmSVJzMUZYVVdGenluODhwT1Y2aEQzMkdidTlfVG9rZW46TWppN2JXQ21mb0JUYVN4YnNPMWN5bENPbjhjXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

**ShareGPT-format Multimodal Dataset**:

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjFkMGRjZjVkYzRkOWEyOWQ2YzA1NTI2NjNkMzlmNDhfaThPZUpoMEZxNEFETGtjb055MERpRmlkR0RqRktpWktfVG9rZW46U3ozOGJXTFdZb05sQWd4bmVWWWNjU09MbmFiXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

**Special ShareGPT-format Dataset: OpenAI Format**

<figure><img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjZiMmQ2NGE3Y2QxNDUzNTg5OWVhYTU4ZDFhOTgxY2Nfb1ZvY0sxVjdldzVacTY2T1h0Rjl0VjFSYmQwTjM5VjJfVG9rZW46VFFnVmJLMEFyb1ljZ1V4VGdUVmNmQTFvbmZlXzE3NDcyMjM0MTA6MTc0NzIyNzAxMF9WNA" alt=""><figcaption></figcaption></figure>

***

#### 2.3 Format Comparison

Below is a detailed comparison between the two dataset formats. You can choose the appropriate format based on your actual requirements:

<table data-header-hidden><thead><tr><th width="146.36328125"></th><th></th><th></th></tr></thead><tbody><tr><td>Comparison Dimension</td><td>Alpaca Format</td><td>ShareGPT Format</td></tr><tr><td>Core Design Purpose</td><td>Single-turn instruction-driven tasks (e.g., Q&A, translation, summarization)</td><td>Multi-turn dialogues and tool invocation (e.g., chatbots, API interactions)</td></tr><tr><td>Data Structure</td><td>JSON objects centered around <code>instruction</code>, <code>input</code>, <code>output</code></td><td>Multi-role dialogue chains (human/gpt/function_call/observation) with <code>conversations</code> list as core</td></tr><tr><td>Dialogue History Handling</td><td>Records history through <code>history</code> field (format: <code>[["instruction", "response"], ...]</code>)</td><td>Naturally represents multi-turn dialogues through ordered <code>conversations</code> list (alternating roles)</td></tr><tr><td>Roles & Interaction Logic</td><td>Only distinguishes user instructions and model outputs, no explicit role labels</td><td>Supports multiple role labels (e.g., <code>human</code>, <code>gpt</code>, <code>function_call</code>), enforces odd-even position rules</td></tr><tr><td>Tool Invocation Support</td><td>No native support, requires implicit description through <code>input</code> or instructions</td><td>Explicit tool invocation through <code>function_call</code> and <code>observation</code>, supports external API integration</td></tr><tr><td>Typical Use Cases</td><td>- Instruction response (e.g., Alpaca-7B) <br>- Domain-specific Q&A <br>- Structured text generation</td><td>- Multi-turn dialogues (e.g., Vicuna) <br>- Customer service systems <br>- Interactions requiring real-time data queries (e.g., weather, calculations)</td></tr><tr><td>Advantages</td><td>- Concise structure, clear task orientation <br>- Suitable for rapid single-turn dataset construction</td><td>- Supports complex dialogue flows and external tool extension <br>- Closer to real human-machine interaction scenarios</td></tr><tr><td>Limitations</td><td>- Requires manual <code>history</code> concatenation for multi-turn dialogues <br>- Lacks dynamic tool interaction capabilities</td><td>- More complex data format <br>- Requires strict adherence to role position rules</td></tr></tbody></table>

***

### Three, Fine-tuning Dataset for Different Purposes

Training sets teach models "basic knowledge", validation sets optimize "learning methods", and test sets evaluate "practical abilities". The three are like a learning cycle of "pre-study, review, and examination", and none can be missing:

* **Training Set** = **Daily Practice Questions** (master knowledge points through extensive practice)
* **Validation Set** = **Mock Exam Papers** (detect learning outcomes, adjust learning methods)
* **Test Set** = **Final Exam** (evaluate real learning abilities)
* **Complete Set** = **All Available Question Banks** (includes the original data of the above three)

***

#### 3.1 Training Set — Teacher Teaches Knowledge

* **Role**: Core learning materials for models
* **Example**: When teaching AI to recognize cats, show it **10,000 labeled cat images** (including different breeds, poses)
* **Key Points**:
  * Must cover various possibilities (day/night, close-up/distant)
  * Equivalent to a student's textbook and exercise book

***

#### 3.2 Validation Set — Learning Effectiveness Check

* **Role**: Prevents rote memorization, tests ability to generalize
* **Typical Scenario**: During training, use **2,000 new cat images** to validate, discover the model mistakenly identifies "hairless cats" as dogs, and adjust the training strategy
* **Core Value**:
  * Select the best model version (e.g., different neural network structures)
  * Adjust hyperparameters (equivalent to changing the learning plan)

***

#### 3.3 Test Set — Final Ability Evaluation

* **Role**: Evaluates model's real-world performance
* **Must Follow**:
  * Absolute isolation principle: The **5,000 cat images** in the test set have never appeared during training
  * Equivalent to a highly confidential exam paper
* **Common Misconceptions**: If the test set is used to repeatedly adjust parameters, it's like cheating on the exam, and the results will be overly optimistic

***

#### 3.4 Complete Set — Data Resource Pool

* **Inclusion Relationship**: Complete set = Training set + Validation set + Test set
* **Partition Proportion** (example):
  * General situation: 70% training + 15% validation + 15% testing
  * Small data scenario: 80% training + 10% validation + 10% testing

***

Below are some frequently asked questions about these three types of datasets:

* **Why can't they be mixed?**: If the test set data leaks into the training set, it's like cheating on the exam, and the model will fail in real-world applications.
* **What if there's not enough data?**: Cross-validation method: Divide the complete set into 5 parts, rotate 4 parts for training and 1 part for validation (similar to "rotating seats for exams"), and synthesize data: Use image flipping, text replacement, and other methods to expand the data volume.
* **Special Scenario Handling**: Time series data: Must be divided according to time order (cannot use random splitting). For example, predicting stock prices, you must use data before 2023 for training and data from 2024 for testing;
