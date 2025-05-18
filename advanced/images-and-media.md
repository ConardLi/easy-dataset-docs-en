---
icon: tent-arrow-left-right
---

# Distilled Datasets

{% hint style="info" %}
The data distillation module supports zero-shot construction of distilled datasets from large parameter models, which can then be used to fine-tune smaller parameter models.
{% endhint %}

### **What is Model Distillation?**

Imagine a "professor" (large model) who is highly knowledgeable but "temperamental": training them requires a huge tuition fee (high training cost), inviting them to give lectures requires a luxurious classroom (high-performance hardware), and each lecture costs a fortune (high inference cost). On the other hand, the "elementary student" (small model) is well-behaved and lightweight (low deployment cost) but has limited knowledge.

**Model distillation** is the process of having the professor "condense" their problem-solving approach into a "cheat sheet" to teach the student.

* The professor doesn't just say "choose A for this question," but provides a probability distribution (e.g., 80% for option A, 20% for option B). This "soft answer" contains their reasoning logic.
* By imitating the professor's approach, the student can learn the core knowledge without incurring high costs, much like using a "problem-solving cheat sheet" to quickly grasp the key points.

{% hint style="success" %}
Simply put: Extract the original dataset and reasoning process from a large model, then fine-tune a smaller model.
{% endhint %}

### **Why Do We Need Model Distillation?**

While large models are powerful, they face two major challenges in practical applications:

1. **High Computational Requirements**: Training a model with hundreds of billions of parameters can cost millions of dollars, making it unaffordable for most companies and individuals.
2. **Deployment Difficulties**: Large models require dozens of GBs of memory to run, which exceeds the capacity of ordinary personal devices.

{% hint style="success" %}
**Core Value of Distillation**: While individuals and small businesses may not have the resources to deploy large-parameter models, they can distill smaller models for specific domains from large models. This significantly reduces deployment costs while maintaining performance in the target domain.
{% endhint %}

### **Examples of Model Distillation**

DeepSeek's series of open-source distilled models:

<figure><img src="../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>

The paper "s1: Simple test-time scaling" by Fei-Fei Li's team mentioned that for just $50, they trained a model comparable to ChatGPT o1 and DeepSeek R1. This was achieved by fine-tuning the open-source model Qwen2.5-32B from Tongyi, using a dataset partially distilled from Google Gemini 2.0 Flash Thinking.

<figure><img src="../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>

The creation of this model involved first using knowledge distillation to obtain reasoning trajectories and answers from the Gemini API, which helped filter out 1,000 high-quality data samples. This dataset was then used to fine-tune the Tongyi Qwen2.5-32B model, ultimately resulting in the well-performing s1 model.

### **Distillation vs Fine-tuning vs RAG**

| Method | Core Idea | Use Case |
|---------|-----------|----------|
| **Distillation** | Small model imitates the problem-solving approach of large models | Lightweight deployment (mobile devices, enterprise private clouds) |
| **Fine-tuning** | "Tutoring" the model with specific data (e.g., medical data) | Vertical domain customization (e.g., legal, medical Q&A) |
| **RAG** | Model "cheats" by calling external knowledge bases | Enterprise document retrieval (e.g., internal training materials) |

### **Basic Process of Distillation**

1. **Prepare the "Cheat Sheet" (Soft Label Generation)**
   * The "professor" first "solves the problems": Input raw data (e.g., "this movie is great") into the large model to generate probability distributions.
2. **Student "Practices" (Model Training)**
   * The small model takes the same data and outputs its own predictions (e.g., "85% positive, 15% negative"), then compares them with the professor's "cheat sheet" to calculate the difference (loss function).
   * Through repeated parameter adjustments (backpropagation), the small model's answers gradually align with the professor's thinking.
3. **Incorporate "Standard Answers" (Combining Soft and Hard Labels)**
   * The small model needs to learn both the professor's approach (soft labels) and ensure accuracy on basic questions (hard labels, e.g., "a cat is a cat"). The balance between the two is controlled by a coefficient (α) to prevent overfitting.

### Using Easy Dataset to Construct Distilled Datasets

{% hint style="success" %}
### What Problems Can Easy Dataset Solve? Distilling datasets from large models for specific domains: For example, if we want to distill a small Traditional Chinese Medicine model based on DeepSeek R1's reasoning process, we first need to extract a domain dataset related to "Traditional Chinese Medicine" from DeepSeek R1.
{% endhint %}

### Approach to Distilled Datasets

In the model distillation process, dataset construction is crucial as it directly determines the quality of the distilled model. The following requirements must be met:

* **Task Scenario Coverage**: The dataset should align with the true distribution of the original task (e.g., image classification, natural language processing) to ensure the features learned by both teacher and student models are meaningful.
* **Diversity and Balance**: The data should include sufficient sample diversity (e.g., different categories, noise levels, edge cases) to prevent the distilled model from having poor generalization due to data bias.

To meet these requirements, we cannot simply extract datasets randomly for specific domains. The approach in Easy Dataset is as follows:

<figure><img src="../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

First, we use the top-level topic (defaulting to the project name) to construct a multi-level domain label hierarchy, forming a complete domain tree. Then, we use the "student model" to extract questions from the leaf nodes of this domain tree. Finally, we use the "teacher model" to generate answers and reasoning processes for each question.

{% hint style="info" %}
In practical tasks, the "student model" used to extract questions and the "teacher model" used to generate answers can be the same model.
{% endhint %}

### Manual Dataset Distillation

Let's create a new project for Physical Education and Sports:

{% hint style="info" %}
In data distillation tasks, the project name will be used as the default top-level distillation topic, so choosing a good project name is crucial.
{% endhint %}

<figure><img src="../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

Then, we go to the data distillation module and click to generate top-level tags:

<figure><img src="../.gitbook/assets/image (102).png" alt=""><figcaption></figcaption></figure>

This operation allows us to generate N subtopics (tags) from the top-level topic (defaulting to the project name). The number of subtopics can be customized. After the task succeeds, a preview of the tags will be generated in the dialog:

<figure><img src="../.gitbook/assets/image (103).png" alt=""><figcaption></figcaption></figure>

We can click "Add Sub-tag" on each subtopic to continue generating multiple levels of subtopics:

<figure><img src="../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>

To ensure the relevance of generated subtopics, the complete tag path will be passed when generating multi-level subtopics:

<figure><img src="../.gitbook/assets/image (105).png" alt=""><figcaption></figcaption></figure>

After building the multi-level domain label tree, we can start extracting questions from the leaf tags:

<figure><img src="../.gitbook/assets/image (106).png" alt=""><figcaption></figcaption></figure>

We can choose the number of questions to generate. Additionally, the complete domain label path will be passed when extracting questions:

<figure><img src="../.gitbook/assets/image (107).png" alt=""><figcaption></figcaption></figure>

After generation is complete, we can preview the questions:

<figure><img src="../.gitbook/assets/image (108).png" alt=""><figcaption></figcaption></figure>

We can see the generated questions from the leaf nodes of the domain tree:

<figure><img src="../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

Then, we can click to generate answers for each question:

<figure><img src="../.gitbook/assets/image (110).png" alt=""><figcaption></figcaption></figure>

We can also go to the question management module to batch generate answers for the generated questions (distilled questions will be displayed as "Distilled Content" by default since they are not associated with text chunks):

<figure><img src="../.gitbook/assets/image (111).png" alt=""><figcaption></figcaption></figure>

### Automatic Dataset Distillation

If you don't need fine-grained control over each step mentioned above, you can choose fully automatic dataset distillation:

<figure><img src="../.gitbook/assets/image (112).png" alt=""><figcaption></figcaption></figure>

In the configuration box, we can see the following options:

* Distillation topic (defaults to project name)
* Number of levels for the domain tree (default is 2)
* Number of tags to generate per level (default is 10)
* Number of questions to generate per sub-tag (default is 10)

<figure><img src="../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

After the task starts, we can see detailed progress including the specific progress of building tags, questions, and answers:

<figure><img src="../.gitbook/assets/image (114).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
This will also follow the maximum concurrency limit set in "Project Settings - Task Settings".
{% endhint %}
