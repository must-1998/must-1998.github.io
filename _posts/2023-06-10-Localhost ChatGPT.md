---
title: 本地搭建 ChatGPT
author: xiaoma
date: 2023-06-10 11:33:00 +0800
categories: [工具效率]
tags: [ChatGPT,AI]
math: true
mermaid: true
image:
  path: /assets/images/chatgpt.jpg
  lqip: /assets/images/lazyload.jpg
  alt: ChatGPT
---

ChatGPT以其强大的信息整合和对话能力惊艳了全球，在自然语言处理上面表现出了惊人的能力，ChatGPT相关的工具也成为人们工作学习的得力帮手。但受限于国内网络的影响，在国内使用ChatGPT收到诸多的限制和不便，好在我们可以站在巨人的肩膀上，去享受科技带来的乐趣！

## ChatGPT简介

> 以下内容来自`ChatGPT`。
{: .prompt-tip }

ChatGPT 是一种基于 OpenAI 的 GPT-3.5 模型的聊天型人工智能助手。它是一个强大的自然语言处理模型，可以理解和生成人类语言，以实现对话和提供有用的回答。

ChatGPT 被广泛应用于各种场景，包括：

1. 问题回答：ChatGPT 可以回答关于广泛主题的问题，例如常见知识、科学、历史、文化等。它能够理解问题的语义并提供准确的答案。
2. 任务辅助：ChatGPT 可以帮助执行各种任务，例如日程安排、提供建议、制定计划等。您可以向它提出关于您需要完成的任务的指示，并获得相应的帮助。
3. 创意生成：ChatGPT 可以帮助您生成创意、提供灵感，例如写作、设计、编程等领域。您可以向它提出问题或请求，以获得创造性的建议和想法。
4. 学习辅助：ChatGPT 可以作为学习的伴侣，回答学术问题、解释概念、提供学习资源等。您可以与它进行交互，获取额外的解释和学习资料。

需要注意的是，尽管 ChatGPT 在许多情况下能够提供有用的答案和建议，但它仍然是一个语言模型，有时可能会生成不准确或不完全合乎预期的回答。在关键任务和决策中，建议仍然需要经过人类的验证和判断。

为了提供更好的体验，ChatGPT 基于事先训练的模型，并使用大量的文本数据进行训练，以便具备广泛的知识和语言理解能力。然而，它的知识截止日期为
2021 年，因此某些最新的信息可能不在其知识范围之内。

总而言之，ChatGPT 是一个功能强大的聊天型人工智能助手，能够在多个领域为用户提供有用的回答和支持。通过与它进行对话，您可以获得问题解答、任务辅助、创意生成和学习辅助等方面的帮助。

## 本地安装ChatGPT

1. 下载并安装Docker [【官网】](https://www.docker.com/)

   安装完成后，打开Docker可能会提示需要升级当前的Windows子系统：

   ![Docker](/assets/images/docker-wsl.jpg){: width="900" height="600" }

   按照页面提示，在`CMD`中输入以下代码，等待更新完成即可

    ```bash
    wsl --update
    ```

2. 使用开源项目：潘多拉(Pandora) [【Github】](https://github.com/pengzhile/pandora)

3. 一键安装命令：

    ```bash
    #拉取远程项目
    docker pull pengzhile/pandora
    ```
    
    ```bash
    #运行本地项目
    docker run  -e PANDORA_CLOUD=cloud -e PANDORA_SERVER=0.0.0.0:8899 -p 8899:8899 -d pengzhile/pandora
    ```

    也可以在Docker Desktop中手动启动：

    ![Docker Run](/assets/images/docker-chatgpt.jpg){: width="900" height="600" }

4. 获取Access TOKEN：[http://chat.openai.com/api/auth/session](http://chat.openai.com/api/auth/session)

5. 访问本地链接：http://127.0.0.1:8899 即可搞定！
