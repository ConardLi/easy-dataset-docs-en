---
icon: wand-magic-sparkles
---

# Dataset Generation

### Generate a Single Dataset

Click on the magic wand 🪄 icon on a single question to generate an answer (construct a dataset) for that question:

<figure><img src="../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

After generating an answer for the question, the number of answers already generated will be displayed on the right side (a single question can generate multiple answers):

<figure><img src="../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Easy DataSet generates answers based on the question + the text block corresponding to the question + domain tags together, to ensure the relevance of the answer to the literature itself.
{% endhint %}

When a reasoning model is selected in the upper right corner, the chain of thought (COT) in the model's reasoning process will be preserved:

<figure><img src="../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

You can filter questions with generated answers and questions without generated answers:

<figure><img src="../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

### Batch Generate Datasets

You can multi-select or select all questions to batch produce answers:

<figure><img src="../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

You can view the progress of batch tasks:

<figure><img src="../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
When a batch task is in progress, closing or refreshing the current page will interrupt the task. You can open a new page to check the already generated answers in dataset management.
{% endhint %}

### Dataset Generation Configuration

The number of concurrent tasks in Task Settings - Question Generation Settings can still control the maximum number of concurrent tasks for batch dataset generation:

<figure><img src="../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
The larger the maximum number of concurrent tasks, the faster the dataset generation task, and vice versa. Pay attention to the maximum concurrency limit of the model provider.
{% endhint %}
