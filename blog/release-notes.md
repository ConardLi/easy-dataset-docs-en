---
icon: up
---

# Release Notes

{% hint style="info" %}
Sync: [https://github.com/ConardLi/easy-dataset/releases/](https://github.com/ConardLi/easy-dataset/releases/)
{% endhint %}

### [1.3.0-beta.1] 2025-05-06

**This update makes significant optimizations to the storage method, reconstructing local file storage as local database storage, greatly improving the user experience for large amounts of data. Due to the large changes made, a beta version is released for everyone to experience. If you encounter any issues while using this version, please submit feedback through Issues to help us further improve the product.**

**🔧 Fixes**

1. Fixed the issue of unexpectedly generating COT during dataset optimization
2. Fixed the issue of processing removed files on the text processing page, causing errors

**⚡ Optimizations**

1. Reconstructed local file storage as local database storage, greatly optimizing the user experience for large amounts of data
2. Randomly removed question marks from problems (configurable)
3. Optimized multiple functional experiences

**✨ New Features**

1. Added local log storage to the client, allowing users to open the log directory to troubleshoot issues
2. Added a cache clearing function to the client, allowing users to clear historical log files and backed-up database files

***

### [1.2.5] 2025-04-13

**🔧 Fixes**

1. Fixed the issue of the model configuration error on the first configuration
2. Fixed the issue of Docker image packaging errors

***

### [1.2.4] 2025-04-12

**⚡ Optimizations**

1. Used the OPEN AI SDK to reconstruct the model interaction interface, improving compatibility

**✨ New Features**

1. Supported visual model configuration
2. Supported using custom visual models to parse PDFs, with higher accuracy
3. Model testing supported sending images to test visual models
4. Dataset details page supported viewing belonging text blocks
5. Supported users editing text blocks themselves
6. Supported downloading and previewing parsed Markdown files

***

### [1.2.3] 2025-03-30

**⚡ Optimizations**

1. Enhanced the default maximum output token limit of the model
2. Removed the update failure pop-up window
3. Removed some interfering error log outputs

**✨ New Features**

1. Supported one-click opening of the client data directory
2. Supported model temperature and maximum generated token number configuration
3. Supported two types of PDF file parsing (basic parsing and MinerU parsing)
4. Supported exporting datasets in CSV format

***

### [1.2.2] 2025-03-24

**🔧 Fixes**

1. Fixed the issue of unable to select problems and delete problems failing in the domain tree view
2. Fixed the issue of the upgrade link to the new version possibly being inaccurate

**⚡ Optimizations**

1. Removed extra line breaks from answers and thought chains
2. Removed the update failure pop-up window and the update download link for the latest installation package

**✨ New Features**

1. Literature management supported filtering generated and ungenerated problems

***

### [1.2.1] 2025-03-23

**🔧 Fixes**

1. Fixed the issue of inaccurate text block sorting

**⚡ Optimizations**

1. Lowered the default concurrency to 3 (solving the problem of triggering some model flow limits)
2. Optimized problem generation prompts, improving problem generation quality
3. Lowered the minimum split character number to 100 and raised the maximum split character number to 10000
4. When the model did not output in the standard format, the log added the original output information

**✨ New Features**

1. Supported editing problems and customizing problems
2. Supported using datasets directly in LLaMa Factory
3. Supported configuring user-defined prompts

***

### [1.1.6] 2025-03-19

**🔧 Fixes**

1. Fixed the issue of extractThinkChain errors
2. Fixed the issue of NPM dependency deprecation
3. Fixed the issue of problem filtering and full selection linkage

**⚡ Optimizations**

1. Optimized the operation of rebuilding the domain tree after deleting literature when uploading multiple literatures
2. The client opened by default in maximized mode, no longer full-screen
3. Optimized the content of thought chains, removing the rhetoric of reference literature

***

### [1.1.5] 2025-03-18

**🔧 Fixes**

1. Fixed the issue of the project list being empty due to caching
2. Fixed the issue of the problem split character number configuration not taking effect
3. Fixed the issue of some special file names causing errors
4. Fixed the issue of some loading states being invalid

**⚡ Optimizations**

1. The client opened external links by default, jumping to the browser
2. Continued to optimize the success rate of dataset result generation
3. Optimized the performance of displaying domain trees for a large number of problems

**✨ New Features**

1. New projects could choose to reuse model configurations from other projects
2. Single projects supported uploading multiple files (shared domain trees)
3. Problem management added filtering for generated and ungenerated datasets
4. Supported uploading docx type files
