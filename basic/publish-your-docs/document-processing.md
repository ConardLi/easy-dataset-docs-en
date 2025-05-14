---
icon: book
---

# Document Processing

{% hint style="info" %}
This module is used to process domain literature in various formats into data structures that can be understood by models.
{% endhint %}

### File Types

Currently, the platform supports processing literature in four formats: **Markdown, PDF, DOCX, and TXT**:

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
Models understand Markdown literature with good structural organization best. It is recommended to prioritize uploading Markdown files.
{% endhint %}

### PDF Processing

Due to the special nature of PDF format, the platform supports four different PDF processing methods for different scenarios. When literature containing PDF format is uploaded, a dialog box will appear:

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

#### Basic Parsing

Focuses on quickly identifying key outlines of simple PDF files. It is efficient for processing well-structured plain text reports and simple documentation, but cannot accurately parse files containing complex content such as large numbers of formulas and charts.

#### MinerU API Parsing

You can configure the MinerU API Key through "Settings - Task Settings" to call the MinerU API for parsing. It can deeply parse complex PDF files containing formulas and charts, suitable for academic papers, technical reports, and other scenarios. The more complex the file, the slower the processing speed. You can apply for a MinerU API Key through [https://mineru.net/apiManage/token](https://mineru.net/apiManage/token) (note that the validity period is 14 days, after which you need to reconfigure).

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

#### MinerU Online Platform Parsing

Redirects to the MinerU platform: [https://mineru.net/OpenSourceTools/Extractor](https://mineru.net/OpenSourceTools/Extractor), where users can parse PDFs and download Markdown files, then return to the platform to re-upload them.

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

#### Custom Vision Model Parsing

Can recognize complex PDF files, including formulas and charts. This method requires adding vision model configuration in the model configuration to parse PDF files through a custom vision model. Parsing rules and model parameters can be customized according to specific needs to adapt to different types of complex PDF files.

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

When choosing MinerU API parsing or custom vision model parsing, the PDF processing time may be longer, please wait patiently:

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption><p><br></p></figcaption></figure>

You can configure the maximum number of concurrent custom vision models and the maximum number of pages to process simultaneously through "Settings - Task Settings". The more concurrent models, the faster the processing speed, but please consider the concurrency limit of the model provider.

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

### Text Segmentation

Before uploading, please select the model in the top right corner, otherwise, the processing will fail:

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Note that there is no need to select a reasoning model (such as DeepSeek-R1) in this step. Selecting a normal question-answering model, such as Doupai or Qianwen, is sufficient. Reasoning models will not provide any advantages in this step and will slow down the processing speed.
{% endhint %}

After uploading, the platform will intelligently segment the text into blocks, and we can see the segmented text blocks and the number of characters in each block:

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

We can view the details of each text block:

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

We can edit each text block:

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

For more information on the principles of text segmentation and how to customize segmentation rules to adapt to different literature structures, please refer to the "[Custom Segmentation](../../advanced/editor.md)" chapter.

### Literature Management

We can filter the text blocks generated for a specific literature:

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

We can preview the literature details (converted to Markdown), download the literature (Markdown), and delete the literature:

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Preview the literature:

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>
