---
icon: face-glasses
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Product Introduction

{% hint style="success" %}
&#x20;                                                [**Easy Dataset**](https://github.com/ConardLi/easy-dataset) **is a powerful large model dataset creation tool.**
{% endhint %}

<figure><img src=".gitbook/assets/bg2.png" alt=""><figcaption></figcaption></figure>

### Why This Tool?

Currently, various industries are actively exploring fine-tuning large models for their specific sectors. The fine-tuning process itself is not difficult, and there are many mature tools available in the market. The challenging part is the initial dataset preparation stage. The quality of the dataset directly determines the effectiveness of the model after fine-tuning. Building high-quality domain datasets consistently faces multiple challenges, and people generally encounter the following problems when building datasets:

{% hint style="danger" %}
* Complete lack of knowledge on how to proceed, currently doing everything manually and wanting to improve efficiency
* Directly giving documents to AI, but AI performs poorly when generating Q&A pairs for large files
* AI has context limitations, cannot generate too many questions at once, and generates duplicate questions when done in batches
* Already have compiled datasets but want a place to manage them in bulk for annotation and validation
* Have specific domain requirements for datasets but don't know how to build domain tags
* Want to fine-tune reasoning models but don't know how to construct Chain-of-Thought (COT) in the fine-tuning dataset
* Want to convert from one dataset format to another but don't know how to do the conversion
{% endhint %}

To solve these problems, **Easy DataSet was created**, providing a systematic solution that implements a complete closed-loop from literature parsing to dataset construction, annotation, export, and evaluation. Below are the problems the tool aims to solve:

{% hint style="success" %}
* Support multiple literature processing methods to convert various formats of literature into formats that models can understand
* Achieve AI-assisted dataset generation without losing accuracy
* Solve truncation problems caused by model context limitations
* Construct datasets in bulk, generate COT, and avoid generating duplicate datasets
* Build domain tags and organize datasets according to domain trees
* Effectively manage datasets for quality verification and other operations
* Easily convert generated datasets into different formats, such as Alpaca and ShareGPT formats
* Effectively evaluate models based on datasets
{% endhint %}

### Design Approach

Easy DataSet uses a **project-based** approach as its core unit, covering the entire chain from "literature processing-question generation-answer construction-tag management-data export":

<figure><img src=".gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

### Core Modules

* **Model Configuration Center**: Supports OpenAI format APIs (such as OpenAI, DeepSeek, various third-party model providers) and local models (Ollama), with built-in model testing Playground, supporting multi-model comparison.
* **Intelligent Literature Processing**: Uses the "Section-Aware Recursive Chunking" algorithm, implements semantic-level segmentation based on Markdown structure, ensures complete content in each chunk (configurable minimum/maximum length), accompanied by outline extraction and summary generation.
* **Domain Tag System**: AI automatically generates two-level domain trees (such as "Sports-Football"), supports manual correction, binds precise tags to each Q&A pair, reducing duplication rate.
* **Intelligent Data Generation**: Extracts questions from domain information, intelligently constructs data based on questions + domain information, and supports multi-dimensional data annotation and multi-format data export.

***

### Data Engine

* **Batch Question Generation**: Based on text block semantics, dynamically generates questions according to character density (configurable), supports batch creation and interruption recovery.
* **Intelligent Answer Construction**: Generates answers associated with original text blocks, supports reasoning models (such as DeepSeek-R1) to generate answers with Chain of Thought (COT).
* **Quality Verification Mechanism**: Provides batch deletion, manual editing, and AI optimization (automatic polishing with input instructions) of questions/answers to ensure data usability.

***

### Format Ecosystem

* **Multi-format Export**: Supports Alpaca, ShareGPT standard formats, custom field mapping, including domain tags and COT information.
* **Dataset Marketplace**: Aggregates multiple platform data sources such as HuggingFace and Kaggle, supports one-click keyword search, solving the initial problem of "where to get data."
