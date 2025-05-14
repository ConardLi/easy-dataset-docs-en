---
icon: question
---

# FAQ

### Q: How to generate an English dataset?

<img src="https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=ODUzZmFmYThhODVkZjM4NjUyNWYzZWMyYzM1NzlmNDFfRkRoQmROWFA2STFIZUI5dWlJaklSbmhGOHJRNUROZXVfVG9rZW46VEJzbGJvcWEwb1lNa2h4MDQzQWMwWlcybktiXzE3NDcyMjMyMDY6MTc0NzIyNjgwNl9WNA" alt="" data-size="original">

The system will decide the final language of the generated dataset based on the current user's language selection. Currently, it supports Chinese and English. The default language environment is Chinese. If you need to generate an English dataset, you need to manually switch to English.

***

### Q: Can't find the desired model provider and model in the model configuration?

![](https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=N2U0NTNjZGZhYjY4YTBhZmM1ZjVjMzZmYzIwODc1YmZfTEl0ZXYyZk5aeUlMc1E0NjlxZjMzQjEwRTFGVThzNnZfVG9rZW46WGMwZ2J1ZHZSb0NjQlZ4TUhIcGMySFdZbndkXzE3NDcyMjMyMDY6MTc0NzIyNjgwNl9WNA)

Currently, it supports **OpenAI standard protocol** model access, compatible with Ollama. The system only has some common model configurations built-in. If you can't find the desired model, you can customize the **model provider**, **model name**, **API address**, and **key**.

***

### Q: The model test is fine, but it reports an error when generating questions or datasets?

In many cases, the system requires the model to output in a specified JSON format. If the model's understanding ability or context length is insufficient, the output may be unstable. It is recommended to replace it with a model with a larger parameter quantity and longer context length.

***

### Q: The batch task processing speed is too slow?

The processing speed of the task is largely determined by the processing speed of the selected model. If it is a local model, please check the resource utilization rate. If it is a remote model, it is recommended to replace it with a faster and more stable platform.

***

### Q: The batch task is interrupted suddenly, and it starts to complete quickly at a certain node?

![](https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=Nzg1NzA2YzE2NGNmYzZiZjRkNjIxZjE0Y2ZkYzhiY2Vfa3N5QzBqTnR6bXJsZ0VnSkhaTTcxakl2S1oxT1JnSm5fVG9rZW46WWpibmI4eVBhbzc3WnR4MU41T2NJSEVGbmxnXzE3NDcyMjMyMDY6MTc0NzIyNjgwNl9WNA)

It is likely that the model's rate limiting strategy has been triggered, which is common in unpaid Silicon Flow and free OpenRouter models. You can manually reduce the concurrent processing number in the task configuration, which is currently set to 5 by default.

***

### Q: The questions or datasets are not output in the expected style?

![](https://rncg5jvpme.feishu.cn/space/api/box/stream/download/asynccode/?code=MjllODY4ZTQwNDRjN2M5NzdjODNkOTc1N2YyNDc0NmJfbTlyUDhvaHM4eEZWSTZHa0tnWHA1Zm1hbUcxRWNGZmpfVG9rZW46QlBIVmJEZ01Zb2hVNGp4YVZBRGNTUE1QbkJlXzE3NDcyMjMyMDY6MTc0NzIyNjgwNl9WNA)

You can add custom prompt words in the project configuration - prompt word configuration to actively intervene.
