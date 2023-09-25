---
title: 爬虫爬取艾瑞咨询研究报告
author: xiaoma
date: 2023-09-25 23:33:00 +0800
categories: [ 编程实战,网络爬虫 ]
tags: [ 爬虫 ]
math: true
mermaid: true
image:
  path: /assets/images/pexels-s-migaj-746386.jpg
  lqip: /assets/images/lazyload.jpg
---

艾瑞咨询持续深耕商业决策服务领域，是一家助力客户提升认知水平、盈利能力和综合竞争力的企业。本文档介绍了如何使用Python从艾瑞网爬取图片并将其生成为一个PPT（PowerPoint）文件。代码使用了多个库，包括requests、BeautifulSoup、Pillow和python-pptx。

## 需求明确
我们的目标是从用户提供的艾瑞网文章页面中提取图片，并将这些图片合并到一个PPT文件中。PPT文件的每一页都包含一张图片，图片的大小与原始图片一致。

## 实现思路

以下是实现目标的主要步骤：
1. 获取用户输入的网页URL。 
2. 使用正则表达式从URL中提取文章编码。 
3. 使用提取的文章编码构建基础URL，该URL用于获取图片。 
4. 发送HTTP GET请求以获取网页内容。 
5. 使用BeautifulSoup解析网页内容，提取文章标题。 
6. 创建一个PPT对象（Presentation）。 
7. 初始化图片编号。 
8. 循环爬取图片，直到遇到返回404错误。 
9. 对于每张图片，发送HTTP GET请求以获取图片内容。 
10. 检查HTTP响应状态码，如果是200，则继续处理图片。 
11. 获取图片的宽度和高度，以确定PPT幻灯片的大小。 
12. 创建PPT幻灯片，设置幻灯片大小与图片大小相匹配。 
13. 在PPT中插入图片。 
14. 增加图片编号，继续爬取下一张图片。 
15. 如果遇到返回404错误，终止爬取。 
16. 保存生成的PPT文件。

## 代码实现
下面是完整的代码以及每一步的详细解释：

```python
import re
import requests
from io import BytesIO
from pptx import Presentation
from pptx.util import Inches
from bs4 import BeautifulSoup
from PIL import Image  # 导入Pillow库的Image模块

# 获取用户输入的网页URL
web_url = input("请输入网页URL：")  # 用户输入文章页面的URL

# 使用正则表达式从网页URL中提取文章编码
match = re.search(r'/(\d+)\.shtml$', web_url)  # 使用正则表达式从URL中提取文章编码
if match:
    article_number = match.group(1)  # 提取文章编码
else:
    print("无法从URL中提取文章编码。")
    # 用户输入文章编号
    article_number = input("请输入文章编号：")  # 如果无法从URL中提取，要求用户手动输入文章编号

# 定义基础URL
base_url = 'https://pic.iresearch.cn/rimgs/{}/{}.jpg'

try:
    web_response = requests.get(web_url)  # 发送HTTP GET请求以获取网页内容
    web_response.raise_for_status()  # 检查HTTP响应状态
    soup = BeautifulSoup(web_response.content, 'html.parser', from_encoding='GBK')  # 使用BeautifulSoup解析HTML
    title = soup.head.title.string.strip()  # 从页面标题中提取文章标题
    pptx_filename = f'{title}.pptx'  # 构建PPT文件名
except requests.exceptions.RequestException as e:
    print(f"无法获取网页标题: {e}")
    pptx_filename = f'images_{article_number}.pptx'

# 创建一个PPT文件
prs = Presentation()

# 初始化图片编号
current_num = 1

# 循环爬取图片，直到遇到返回404错误
while True:
    img_url = base_url.format(article_number, current_num)  # 构建图片URL
    
    # 发送GET请求获取图片内容
    img_response = requests.get(img_url)
    
    # 检查HTTP响应状态码
    if img_response.status_code == 200:
        img_bytes = BytesIO(img_response.content)  # 将图片内容存储在内存中的字节流中
        
        # 获取图片的宽度和高度
        with Image.open(img_bytes) as img:
            img_width, img_height = img.size
        
        # 创建PPT幻灯片，设置幻灯片大小与图片大小相匹配
        prs_width = Inches(img_width / 72)  # 将像素转换为Inches
        prs_height = Inches(img_height / 72)
        prs.slide_width = prs_width
        prs.slide_height = prs_height
        
        # 在PPT中插入图片
        slide = prs.slides.add_slide(prs.slide_layouts[5])
        left = top = Inches(0)
        slide.shapes.add_picture(img_bytes, left, top, width=prs_width, height=prs_height)
        
        print("第{}页爬取完毕！！！".format(current_num))
        # 增加图片编号，继续爬取下一张图片
        current_num += 1
    elif img_response.status_code == 404:
        # 遇到返回404错误，终止爬取
        break

# 保存PPT文件
prs.save(pptx_filename)
print(f'生成的PPT文件保存为 {pptx_filename}')
print("Job Finished.")
```
