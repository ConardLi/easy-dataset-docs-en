---
icon: comments-question-check
---

# Question Generation

{% hint style="info" %}
Extract questions from the split text blocks and establish domain tags for the questions.
{% endhint %}

### Generate Questions from a Single Text Block

<figure><img src="../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

After the task is completed, you can view the generated questions in the text block.

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

You can filter text blocks with generated questions and text blocks without generated questions:

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

### Batch Question Generation

You can batch select or select all text blocks, and construct questions in batch:

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

You can view the progress of batch tasks in real-time:

<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
When a batch task is in progress, closing or refreshing the current page will interrupt the task. You can open a new page to check the already generated questions in question management.
{% endhint %}

### Question Generation Configuration

How many questions are generated for each text block is determined by the maximum length for generating questions in "Project Settings - Task Settings". The default setting is to generate one question per 240 characters. For text blocks of around 2000 characters, about 8 questions will be generated. You can flexibly adjust this according to the information density of your literature:

<figure><img src="../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

You can also control the proportion of question marks (?) to be removed in the generated questions (default will remove 60%).

<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
In actual Q&A tasks, users' questions do not always include question marks. Removing a certain percentage of question marks helps improve fine-tuning effects.
{% endhint %}

You can control the maximum number of concurrent tasks in batch tasks (default maximum concurrency is 5 tasks).

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
Note that some model providers will limit the maximum number of concurrent tasks. Setting too large a value may cause batch tasks to fail. It is recommended to flexibly test and adjust.
{% endhint %}
