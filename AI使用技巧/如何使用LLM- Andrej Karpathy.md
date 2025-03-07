#  [Andrej Karpathy](https://www.youtube.com/andrejkarpathy)教你使用LLM

## 理解LLM是什么？

将用户的文本变为LLM可识别的token，然后LLM会根据这些token进行计算，找到关于此话题高相关的token进行拼接，然后将token转换为文字，响应给用户。

注意： 计算token的[网址](https://tiktokenizer.vercel.app/)；

## 如何识别大语言模型的幻觉？

对于计算：

- chatgpt调用python进行计算；
- claude使用javascript进行计算；
- grok3有幻觉，只是给出一个大概的答案；
- gemini与grok相同；

## 如何获得更 准确的答案？

比较各个LLM的结果；

## 各种应用场景

1. 生成文章 概念图

   当你读书时，你想快速掌握这张内容，那么可以将某一张内容复制到LLM中，然年后让他生成概念图；

>Prompt：这是《书名》的第X章，请你使用概念图总结上面文本；

2. 总结对话文本为图片

当你在一个对话中进行很多次互动后，你可以尝试将其生成为图片。

如果你的模型支持生成图片，你可以使用如下Prompt进行总结：

>Promot：请你生成一幅图总结今天；

3. 使用chatgpt学习外语

做一些定制的chatgpt，已解决你在特定方面的问题；

比如你想了解某个句子是如何翻译出来的？可是使用如下Prompt：

>我将提供你一个句子，请你首先将其翻译为中文，然后告诉我你是如何进行分词、分句的；
>
><example1>
>
><input>
>
>I love you
>
><input/>
>
><output>
>
>中文：我爱你
>
>I：主语，
>
>am：谓语
>
>You：宾语
>
><output/>
>
><example/>
>
>



