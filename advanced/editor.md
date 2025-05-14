---
icon: pen-to-square
---

# Text Spliting

{% hint style="info" %}
In many application scenarios, document splitting is an extremely critical preprocessing step. Its core operation is to break down long texts into smaller, more manageable chunks. This approach has many benefits, such as enabling documents of different lengths to be processed in a unified way, solving the problem of model input length limitations, and improving the quality of text representation in retrieval systems. There are various methods for splitting documents, each with its own advantages.
{% endhint %}

In Easy Dataset, you can customize different chunking strategies for literature processing through "Settings - Task Settings - Chunking Settings".

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

### Why Chunk Text?

The purpose of text chunking is to split documents into small segments, making it easier for subsequent applications to use. Through chunking, we can:

* **Solve the problem of inconsistent document lengths**: In real document libraries, text lengths vary. Splitting ensures that all documents can be processed in the same way.
* **Break through model limitations**: Many models have a maximum input length limit. After splitting documents, those that were too long to use can now be processed.
* **Improve representation quality**: For long documents, extracting too much information at once may reduce quality. Splitting allows each chunk to be more precise and targeted.
* **Increase retrieval accuracy**: In information retrieval systems, splitting documents enables more granular search results, allowing queries to match relevant parts of documents more accurately.
* **Optimize use of computing resources**: Processing small text chunks saves memory and allows for more efficient parallel task processing.

### Fixed-Length Chunking

The simplest and most intuitive splitting strategy is to divide by document length. This method is simple and effective, ensuring that each chunk does not exceed the set maximum length. The advantages of length-based splitting include being easy to implement and understand, producing chunks of relatively consistent length, and being easily adjustable for different model requirements. Length-based splitting can be further divided into:

* **Token-based splitting**: Split text according to the number of tokens, which is very useful when working with language models.
* **Character-based splitting**: Split text based on the number of characters, which maintains good consistency across different types of text.

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

When using fixed-length chunking, you can configure:

1. **separator: "\n\n"**: Specifies the boundary marker for splitting text. By default, two consecutive line breaks (\n) are used as the separator. This means the text will be split at every blank line, breaking the original content into independent paragraph chunks. For example, an article with multiple blank lines will be split into several subtexts by paragraph. Adjusting the separator (such as changing to "\n" or "---") allows flexible control over the granularity of splitting, suitable for different text formats (such as code, Markdown documents, etc.).
2. **chunkSize: 1000**: Defines the maximum character length for each chunk. After splitting by the separator, if a chunk exceeds this value, it will be further divided into smaller chunks, ensuring all chunks do not exceed the specified size. For example, a paragraph with 3000 characters will be split into up to 3 chunks (each ≤1000 characters). This parameter directly affects the granularity of subsequent processing: smaller values generate more, finer chunks suitable for scenarios requiring precise context; larger values reduce the number of chunks, retaining more complete semantic units.
3. **chunkOverlap: 200**: Controls the number of overlapping characters between adjacent chunks. At the end of each chunk, a specified number of characters are retained as an overlap with the next chunk. For example, when chunkOverlap: 200, the last 200 characters of the previous chunk will be repeated at the beginning of the next chunk. This design ensures semantic continuity, preventing key information from being lost due to splitting, which is especially important for context-dependent tasks (such as retrieval and Q&A). The overlap area acts as a transition buffer, helping the model access the context of adjacent content when processing a single chunk.

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If the document is relatively simple and lacks obvious structure, this solution is recommended.
{% endhint %}

### Text Structure Chunking

Text is naturally organized into hierarchical structures such as paragraphs, sentences, and words. We can leverage this inherent structure to formulate splitting strategies, ensuring that the chunked text maintains the fluency of natural language, semantic coherence within the chunk, and adapts to different levels of text granularity. The splitter will first try to keep larger units (such as paragraphs) intact. If a unit exceeds the chunk size limit, it will move to the next level (such as sentences). If necessary, this process will continue down to the word level.

Recursive text structure chunking also supports configuring the maximum chunk size, overlap characters, and multiple custom separators:

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If the literature has a relatively complex structure and requires multiple different separators, this solution is recommended.
{% endhint %}

### Document Structure Chunking

Markdown-based document structure chunking is the platform's default chunking strategy:

* First, you need to set the minimum and maximum split lengths for the text block;
* Then, automatically identify chapters (such as `#`, `##`, `###` in Markdown);
* Count the number of words in the identified chapters, and split them into segments when the length is between the minimum and maximum split lengths;
* When encountering overly long paragraphs (exceeding the maximum split length), recursively split the paragraphs to ensure semantic integrity.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If the Markdown file has a good structural division, using this scheme can achieve the best chunking effect.
{% endhint %}

### Code Structure Chunking

When the target text contains a large amount of code, traditional splitting methods are not applicable, and may cause code fragmentation. Easy Dataset also provides a splitting method based on intelligent code semantic understanding, which can choose the target language for chunking:

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### Visual Custom Chunking

When the above chunking strategies cannot meet your needs, you can choose to use the visual custom chunking function. First, find the literature to be chunked and click to view details:

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

After opening the file preview view, click the top right corner to enable custom chunking mode:

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

Select the text at the position where you need to chunk:

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

The top will display the current chunking position, chunk count, and character count for each chunk:

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Click to save the chunk:

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

After saving, it will completely replace the current literature's historical chunking content:

<figure><img src="../.gitbook/assets/image (96).png" alt=""><figcaption></figcaption></figure>
