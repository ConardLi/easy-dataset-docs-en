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

当选择 MinerU API 解析、自定义视觉模型解析时，PDF 处理时间可能较长，请耐心等待：

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption><p><br></p></figcaption></figure>

可通过 「设置-任务设置」 配置自定义视觉模型的最大并发数量，及最多同时处理多少页 PDF，并发数量越大，处理速度也快，注意考虑模型提供商的并发量限制。

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

### 文本分块

在选择好文件和处理方式，点击上传前，注意一定要提前在右上角选择模型，否则会导致处理失败：

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
注意，这一步大家没必要选推理模型（比如 DeepSeek-R1），选择一个普通的问答模型比如豆包、千问都可以，在这一步推理模型并不会起到优势，而且会拖慢处理速度。
{% endhint %}

点击上传后，会将传入的文献进行了智能的文本分割，我们可以在分割列表里看到被拆分好的文本块，以及每个文本块的字数：

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

可以查看每个文本块的详情：

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

可以对每个文本块进行编辑：

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

关于文本分块的原理，以及想自定义分块规则以适应不同的文献结构，可查看：《[自定义分块](../../advanced/editor.md)》 章节。

### 文献管理

可以筛选指定文献已经生成的文本块：

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

&#x20;可预览文献详情（转换为 Markdown），下载文献（Markdown），删除文献：

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

预览文献：

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>
