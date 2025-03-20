---
title: Learning how to write basic Markdown syntax.
date: 2025-03-20 19:54:00 +0800
# date: 2019-08-08 14:10:00 +0800
categories: [Writing, Markdown]
tags: [Writing, Markdown]

author: [sjc]

description: This is a description.
render_with_liquid: true  # for video

mermaid: true  # for mermaid
---

This tutorial will guide you how to write a post in the _Chirpy_ template, and it's worth reading even if you've used Jekyll before, as many features require specific variables to be set.

![img-description](/assets/img/avatar.jpg){: w="200" h="200" }
_Image Caption_

![img-description](/assets/img/avatar.jpg){: w="200" h="200" .left }
<!-- _Image Caption_ -->
![img-description](/assets/img/avatar.jpg){: w="200" h="200" .right }
<!-- _Image Caption_ -->

所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出所以我可以在这里疯狂输出啊



{% include embed/bilibili.html id='BV1FmQfYqEVW' %}  

{% include embed/youtube.html id='Balreaj8Yqs' %}  

> Example line for prompt.
{: .prompt-info }  

`inline code part`

`/path/to/a/file.extend`{: .filepath}

```
This is a plaintext code snippet.
```

```yaml
key: value
```  

```shell
echo 'No more line numbers!'
```
当你想隐藏代码块的行号时，可以为其添加nolineno类：
```shell
echo 'No more line numbers!'
```
{: .nolineno }

```shell
# content
```
{: file="path/to/file" }

{% raw %}
```liquid
{% if product.title contains 'Pack' %}
  This product's title contains the word Pack.
{% endif %}
```
{% endraw %}

```mermaid
graph TD;
    A[开始] --> B[步骤 1]
    B --> C[步骤 2]
    C --> D[结束]
```