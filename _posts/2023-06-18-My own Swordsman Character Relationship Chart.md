---
title: 武林外传人物关系图谱
author: xiaoma
date: 2023-06-18 11:33:00 +0800
categories: [ 随笔杂谈 ]
tags: [ 杂谈 ]
math: true
mermaid: true
image:
  path: /assets/images/my-own-swordsman.jpg
  lqip: /assets/images/lazyload.jpg
  alt: 嘿，兄弟，咋们好久不见你在哪里……
---

最近重温了儿时的经典电视剧《武林外传》，同时又接触了一些基于pyecharts的可视化图表，于是就心血来潮想通过pyecharts来制作一个武林外传人物之间的关系图谱，话不多说，直接开整！

## 预期目标

1. 可视化展示武林外传中主要人物之间的关系，节点以人物头像展示；
2. 人物头像下方展示任务标签信息，包括人物姓名及职位；
3. 鼠标悬停在人物头像上时，突出展示当前人物极其关联人物信息；
4. 鼠标悬停在人物头像上时，可展示人物详细信息，包括姓名、职业、口头禅等。

## 环境准备

开发环境：Anaconda-jupyter notebook <br>
Python: 3.9.7 <br>
相关库：pyecharts==2.0.3

## 数据收集

相关字段：人物姓名、职业、称号、武器、名言、演员、头像链接、是否主角、人物特点

```json
[
  {
    "name": "佟湘玉",
    "symbol": "image://https://bkimg.cdn.bcebos.com/smart/4034970a304e251f294a272ba286c9177e3e53a0-bkimg-process",
    "symbolSize": [60, 60],
    "category": 0,
    "label": opts.LabelOpts(is_show=True, font_size=12, font_weight='bold', color="#000", formatter="{b}\n同福客栈掌柜"),
    "info": "姓名：佟湘玉<br>职业：同福客栈掌柜<br>称号：掌柜的<br>武器：烽火霹雳弹<br>名言：我滴神呀，上帝以及老天爷呀！<br>演员：闫妮<br>特点：抠门，善解人意，明事理"
  }
]
```

数据来源：由于网络上无与此相关的系统性数据，因此数据来源于百度百科，经过手工整理而成。

| **人物** 	 | **职位**      	 | **称号** 	 | **武器**  	 | **口头禅**                  	 |                       **头像链接**                                         	                        | **演员** 	 | **是否主角** 	 |                     **特点**                                           	                      |
|:--------:|:-------------:|:--------:|:---------:|:--------------------------:|:-----------------------------------------------------------------------------------------------:|:--------:|:----------:|:-------------------------------------------------------------------------------------------:|
|  佟湘玉  	  |  同福客栈掌柜    	  |  掌柜的  	  |  烽火霹雳弹 	  |  我滴神呀，上帝以及老天爷呀！         	  | https://bkimg.cdn.bcebos.com/smart/4034970a304e251f294a272ba286c9177e3e53a0-bkimg-process     	 |  闫妮   	  |  是      	  |    抠门，善解人意，明事理                                                                        	     |
|  白展堂  	  |  同福客栈跑堂    	  |  盗圣   	  |  葵花点穴手 	  | 手里捧着窝窝头，菜里没有一滴油……       	  | https://bkimg.cdn.bcebos.com/smart/aa64034f78f0f73639182abf0455b319eac413ad-bkimg-process     	 |  沙溢   	  |  是      	  |       性子爽朗，明白事理，有责任心，胆小                                                            	        |
|  李秀莲  	  |  同福客栈厨师    	  |  李大嘴  	  |  玄铁菜刀  	  |  兄弟你甭说了，这事儿包我身上了。       	  | https://bkimg.cdn.bcebos.com/smart/7a899e510fb30f2484c3ce96c295d143ac4b03cd-bkimg-process     	 |  姜超   	  |  是      	  |                流氓假仗义，假勇假鲁，一心想学武功、总想行侠仗义，只要一出手就必是惹祸                        	                 |
|  郭芙蓉  	  |  同福客栈杂役    	  |  芙妹   	  |  排山倒海  	  |  确定一定以及肯定。              	  | https://bkimg.cdn.bcebos.com/smart/8c1001e93901213fb80ef0e98db621d12f2eb9383ffe-bkimg-process 	 |  姚晨   	  |  是      	  |                     直爽，敢爱敢恨，不计前嫌，刁蛮，懒惰，有时娇气，乱花钱，爱作梦，脑子一根筋，经常上当受骗      	                     |
|  吕轻侯  	  |  同福客栈账房    	  |  秀才   	  |  知识    	  | 子曾经曰过……                 	  | https://bkimg.cdn.bcebos.com/smart/0dd7912397dda144c0b0a361b7b7d0a20df486ac-bkimg-process     	 |  喻恩泰  	  |  是      	  |                      被欺负、吃醋、算帐、拽文、写诗、捐款、线性代数、微积分、高等物理、精细化工、洋文、知识问答 。 	                      |
|  邢育森  	  | 七侠镇37任缁衣捕头 	  |  老邢   	  |  捕头佩刀  	  |  我看好你哟。亲娘嘞！             	  | https://bkimg.cdn.bcebos.com/smart/622762d0f703918ffbedc1125b3d269759eec42e-bkimg-process     	 |  范明   	  |  否      	  |        巡街、蹭吃蹭喝，吃人嘴不软，拿人手不短                                                        	         |
|  燕小六  	  | 七侠镇38任缁衣捕头 	  |  小六   	  |  脱鞋    	  |  帮我照顾好我七舅姥爷和他三外甥女!      	  | https://bkimg.cdn.bcebos.com/pic/72f082025aafa40fa57e050eae64034f79f019ad?x-bce-process       	 |  肖剑   	  |  否      	  |               头脑简单，但是心肠热、装官腔、双手抱拳恭维、打天津快板、唢呐、二胡                            	                |
|  祝无双  	  |  七侠镇唯一女捕快  	  |  超级怨妇 	  |  葵花点穴手 	  |  放着我来！                  	  | https://bkimg.cdn.bcebos.com/smart/b21c8701a18b87d62ec299cb020828381e30fd65-bkimg-process     	 |  倪虹洁  	  |  否      	  |           温柔贤惠、体贴入微、利落仔细、有爱心同情心、明事理                                            	            |
|  白翠萍  	  |  六扇门密使     	  |  白三娘  	  |  葵花点穴手 	  |  无                      	  | https://bkimg.cdn.bcebos.com/smart/86d6277f9e2f070839091dd4ec24b899a801f2d1-bkimg-process     	 |  黄晓娟  	  |  否      	  |                  对亲人如春天般温暖，对敌人如冬天般冷酷无情，多疑，冷静。曾虐待佟湘玉一天多。                  	                  |
|  公孙乌龙 	  |  绝世高手      	  |  公孙乌龙 	  |  传音入密  	  |  善哉，善哉                  	  | https://bkimg.cdn.bcebos.com/smart/0b55b319ebc4b74543a9e9e2b6aa09178a82b801bfb3-bkimg-process 	 |  白志迪  	  |  否      	  | 心狠手辣                                                                                      	 |
|  赛貂蝉  	  |  怡红楼掌柜     	  |  赛掌柜  	  |  偷税漏税  	  |  无                      	  | https://bkimg.cdn.bcebos.com/smart/0dd7912397dda144f1a15f3eb8b7d0a20df48695-bkimg-process     	 |  刘敏   	  |  否      	  |                贪婪，无耻，工于心计，经佟湘玉不计前嫌愿为其赎身一事后洗心革面弃恶从善                        	                 |
|  姬无命  	  |  江湖人士      	  |  盗神   	  |  不详    	  |  是我杀了我                  	  | https://bkimg.cdn.bcebos.com/smart/6a63f6246b600c33537d9e671a4c510fd9f9a11d-bkimg-process     	 |  王磊   	  |  否      	  | 心狠手辣                                                                                      	 |
|  莫小贝  	  |  衡山派掌门     	  |  赤焰狂魔 	  |  隔空打穴  	  | 嫂子…他们欺负我了啦……            	  | https://bkimg.cdn.bcebos.com/smart/bd3eb13533fa828ba61ec80bca4f5634970a314eec81-bkimg-process 	 |  王莎莎  	  |  是      	  |          古灵精怪、幽默耍宝、不爱学习爱拌嘴、独立自主                                                  	          |
|  杨蕙兰  	  |  江湖人士      	  |  惠兰   	  |  寡妇刀   	  |  无                      	  | https://bkimg.cdn.bcebos.com/pic/2934349b033b5bb5c9ea7032ee82c239b6003bf316e7?x-bce-process   	 |  于娟   	  |  否      	  |          喜欢钱，个性凶残，爱喝酒、啥都要就是不要大嘴。                                                	           |
|  断指轩辕 	  |  千堵之王      	  |  断指   	  |  出老千   	  |  我吃的盐比你吃的米还多呢！          	  | https://bkimg.cdn.bcebos.com/pic/55e736d12f2eb938a0457106df628535e5dd6f1d?x-bce-process       	 |  张少华  	  |  否      	  | 教子有方                                                                                      	 |
|  小青   	  |  郭芙蓉丫环     	  |  雌雄双煞 	  |  剑     	  |  无                      	  | https://bkimg.cdn.bcebos.com/smart/faedab64034f78f047a8ee2a7c310a55b2191c43-bkimg-process     	 |  张歆艺  	  |  否      	  | 对小姐忠心                                                                                    	  |
|  小翠   	  |  赛貂蝉丫环     	  |  无    	  |  复读机   	  |  重复赛貂蝉说的话的后面几个字（像个回音音响） 	  | https://bkimg.cdn.bcebos.com/smart/8c1001e93901213fc8de730851e736d12e2e9570-bkimg-process     	 |  蒋卉   	  |  否      	  |           热情、倔强、不服输、本性淳朴善良（赛貂蝉语），记仇                                            	            |
|  展红绫  	  |  六扇门捕头     	  |  红绫   	  |  判官夺命笔 	  |  女人的直觉                  	  | https://bkimg.cdn.bcebos.com/pic/d31b0ef41bd5ad6eddc462820b9d2edbb6fd52669607?x-bce-process   	 |  霍曼迪  	  |  否      	  | 抓贼、追贼                                                                                    	  |

## 可视化

### 完整代码
代码不是特别复杂，也没有什么需要重点拆分出来说明的步骤，所以就直接附上完整代码啦！
```python
from pyecharts import options as opts
from pyecharts.charts import Graph
from pyecharts.commons.utils import JsCode

# 定义节点和边的数据
nodes = [
    {
        "name": "佟湘玉",
        "symbol": "path:///assets/images/demo.jpg",
        "category": 0,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：佟湘玉<br>职业：同福客栈掌柜<br>称号：掌柜的<br>武器：烽火霹雳弹<br>名言：我滴神呀，上帝以及老天爷呀！<br>演员：闫妮<br>特点：抠门，善解人意，明事理"
    },
    {
        "name": "白展堂",
        "symbol": "image://https://bkimg.cdn.bcebos.com/smart/aa64034f78f0f73639182abf0455b319eac413ad-bkimg-process",
        "category": 0,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：白展堂<br>职业：同福客栈跑堂<br>称号：盗圣<br>武器：葵花点穴手<br>名言：手里捧着窝窝头，菜里没有一滴油……<br>演员：沙溢<br>特点：性子爽朗，明白事理，有责任心，胆小"
    },   
    {
        "name": "李秀莲",
        "symbol": "image://https://bkimg.cdn.bcebos.com/smart/7a899e510fb30f2484c3ce96c295d143ac4b03cd-bkimg-process",
        "category": 0,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：李秀莲<br>职业：同福客栈厨师<br>称号：李大嘴<br>武器：玄铁菜刀<br>名言：兄弟你甭说了，这事儿包我身上了。<br>演员：姜超<br>特点：流氓假仗义，假勇假鲁，一心想学武功、总想行侠仗义，只要一出手就必是惹祸"
    },   
    {
        "name": "郭芙蓉",
        "symbol": "image://https://bkimg.cdn.bcebos.com/smart/8c1001e93901213fb80ef0e98db621d12f2eb9383ffe-bkimg-process",
        "category": 0,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：郭芙蓉<br>职业：同福客栈杂役<br>称号：芙妹<br>武器：排山倒海<br>名言：确定一定以及肯定。<br>演员：姚晨<br>特点：直爽，敢爱敢恨，不计前嫌，刁蛮，懒惰，有时娇气，乱花钱，爱作梦，脑子一根筋，经常上当受骗"
    },   
    {
        "name": "吕轻侯",
        "symbol": "image://https://bkimg.cdn.bcebos.com/smart/0dd7912397dda144c0b0a361b7b7d0a20df486ac-bkimg-process",
        "category": 0,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：吕轻侯<br>职业：同福客栈账房<br>称号：秀才<br>武器：知识<br>名言：子曾经曰过……<br>演员：喻恩泰<br>特点：被欺负、吃醋、算帐、拽文、写诗、捐款、线性代数、微积分、高等物理、精细化工、洋文、知识问答 。"
    },    
    {
        "name": "邢育森",
        "symbol": "image://https://bkimg.cdn.bcebos.com/smart/622762d0f703918ffbedc1125b3d269759eec42e-bkimg-process",
        "category": 1,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：邢育森<br>职业：七侠镇37任缁衣捕头<br>称号：老邢<br>武器：捕头佩刀<br>名言：我看好你哟。亲娘嘞！<br>演员：范明<br>特点：巡街、蹭吃蹭喝，吃人嘴不软，拿人手不短"
    },   
    {
        "name": "燕小六",
        "symbol": "image://https://bkimg.cdn.bcebos.com/pic/72f082025aafa40fa57e050eae64034f79f019ad?x-bce-process",
        "category": 1,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：燕小六<br>职业：七侠镇38任缁衣捕头<br>称号：小六<br>武器：脱鞋<br>名言：帮我照顾好我七舅姥爷和他三外甥女!<br>演员：肖剑<br>特点：头脑简单，但是心肠热、装官腔、双手抱拳恭维、打天津快板、唢呐、二胡"
    },   
    {
        "name": "祝无双",
        "symbol": "image://https://bkimg.cdn.bcebos.com/smart/b21c8701a18b87d62ec299cb020828381e30fd65-bkimg-process",
        "category": 1,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：祝无双<br>职业：七侠镇唯一女捕快<br>称号：超级怨妇<br>武器：葵花点穴手<br>名言：放着我来！<br>演员：倪虹洁<br>特点：温柔贤惠、体贴入微、利落仔细、有爱心同情心、明事理"
    },  
    {
        "name": "白翠萍",
        "symbol": "image://https://bkimg.cdn.bcebos.com/smart/86d6277f9e2f070839091dd4ec24b899a801f2d1-bkimg-process",
        "category": 1,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：白翠萍<br>职业：六扇门密使<br>称号：白三娘<br>武器：葵花点穴手<br>名言：无<br>演员：黄晓娟<br>特点：对亲人如春天般温暖，对敌人如冬天般冷酷无情，多疑，冷静。曾虐待佟湘玉一天多。"
    },    
    {
        "name": "公孙乌龙",
        "symbol": "image://https://bkimg.cdn.bcebos.com/smart/0b55b319ebc4b74543a9e9e2b6aa09178a82b801bfb3-bkimg-process",
        "category": 1,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：公孙乌龙<br>职业：绝世高手<br>称号：绝世高手<br>武器：传音入密<br>名言：善哉，善哉！<br>演员：白志迪<br>特点：心狠手辣"
    },   
    {
        "name": "赛貂蝉",
        "symbol": "image://https://bkimg.cdn.bcebos.com/smart/0dd7912397dda144f1a15f3eb8b7d0a20df48695-bkimg-process",
        "category": 1,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：赛貂蝉<br>职业：怡红楼掌柜<br>称号：赛掌柜<br>武器：偷税漏税<br>名言：无<br>演员：刘敏<br>特点：贪婪，无耻，工于心计，经佟湘玉不计前嫌愿为其赎身一事后洗心革面弃恶从善"
    },    
    {
        "name": "姬无命",
        "symbol": "image://https://bkimg.cdn.bcebos.com/smart/6a63f6246b600c33537d9e671a4c510fd9f9a11d-bkimg-process",
        "category": 1,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：姬无命<br>职业：江湖人士<br>称号：盗神<br>武器：不详<br>名言：是我杀了我！<br>演员：王磊<br>特点：心狠手辣"
    },    
    {
        "name": "莫小贝",
        "symbol": "image://https://bkimg.cdn.bcebos.com/smart/bd3eb13533fa828ba61ec80bca4f5634970a314eec81-bkimg-process",
        "category": 0,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：莫小贝<br>职业：衡山派掌门<br>称号：赤焰狂魔<br>武器：隔空打穴<br>名言：嫂子…他们欺负我了啦……<br>演员：王莎莎<br>特点：古灵精怪、幽默耍宝、不爱学习爱拌嘴、独立自主"
    },   
    {
        "name": "杨蕙兰",
        "symbol": "image://https://bkimg.cdn.bcebos.com/pic/2934349b033b5bb5c9ea7032ee82c239b6003bf316e7?x-bce-process",
        "category": 1,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：杨蕙兰<br>职业：江湖人士<br>称号：惠兰<br>武器：寡妇刀<br>名言：无<br>演员：于娟<br>特点：喜欢钱，个性凶残，爱喝酒、啥都要就是不要大嘴。"
    },   
    {
        "name": "断指轩辕",
        "symbol": "image://https://bkimg.cdn.bcebos.com/pic/55e736d12f2eb938a0457106df628535e5dd6f1d?x-bce-process",
        "category": 1,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：断指轩辕<br>职业：千堵之王<br>称号：断指<br>武器：出老千<br>名言：我吃的盐比你吃的米还多呢！<br>演员：张少华<br>特点：教子有方"
    },   
    {
        "name": "小青",
        "symbol": "image://https://bkimg.cdn.bcebos.com/smart/faedab64034f78f047a8ee2a7c310a55b2191c43-bkimg-process",
        "category": 1,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：小青<br>职业：郭芙蓉丫环<br>称号：雌雄双煞<br>武器：剑<br>名言：无<br>演员：张歆艺<br>特点：对小姐忠心"
    },    
    {
        "name": "小翠",
        "symbol": "image://https://bkimg.cdn.bcebos.com/smart/8c1001e93901213fc8de730851e736d12e2e9570-bkimg-process",
        "category": 1,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：小翠<br>职业：赛貂蝉丫环<br>称号：无<br>武器：复读机<br>名言：重复赛貂蝉说的话的后面几个字（像个回音音响）<br>演员：蒋卉<br>特点：热情、倔强、不服输、本性淳朴善良（赛貂蝉语），记仇"
    },    
    {
        "name": "展红绫",
        "symbol": "image://https://bkimg.cdn.bcebos.com/pic/d31b0ef41bd5ad6eddc462820b9d2edbb6fd52669607?x-bce-process",
        "category": 1,
        "label": opts.LabelOpts(is_show=True, font_weight='bold',color="#000",formatter="{b}\n同福客栈掌柜"),
        "info": "姓名：展红绫<br>职业：六扇门捕头<br>称号：红绫<br>武器：判官夺命笔<br>名言：女人的直觉<br>演员：霍曼迪<br>特点：抓贼、追贼"
    },
]
links = [
    {"source": "佟湘玉", "target": "白展堂", "value":"情侣", "symbol":["arrow",""]},
    {"source": "佟湘玉", "target": "李秀莲", "value":"雇主", "symbol":["arrow",""]},
    {"source": "佟湘玉", "target": "郭芙蓉", "value":"雇主", "symbol":["arrow",""]},
    {"source": "佟湘玉", "target": "吕轻侯", "value":"雇主", "symbol":["arrow",""]},
    {"source": "佟湘玉", "target": "莫小贝", "value":"嫂子", "symbol":["arrow",""]},
    {"source": "佟湘玉", "target": "赛貂蝉", "value":"对手", "symbol":["arrow",""]},
    {"source": "白展堂", "target": "佟湘玉", "value":"情侣", "symbol":["arrow",""]},
    {"source": "白展堂", "target": "祝无双", "value":"师兄", "symbol":["arrow",""]},
    {"source": "白展堂", "target": "姬无命", "value":"昔日好友", "symbol":["arrow",""]},
    {"source": "白展堂", "target": "展红绫", "value":"友人", "symbol":["arrow",""]},
    {"source": "白展堂", "target": "白翠萍", "value":"儿子", "symbol":["arrow",""]},
    {"source": "郭芙蓉", "target": "吕轻侯", "value":"情侣", "symbol":["arrow",""]},
    {"source": "郭芙蓉", "target": "佟湘玉", "value":"佣人", "symbol":["arrow",""]},
    {"source": "郭芙蓉", "target": "小青", "value":"主人", "symbol":["arrow",""]},
    {"source": "吕轻侯", "target": "佟湘玉", "value":"佣人", "symbol":["arrow",""]},
    {"source": "吕轻侯", "target": "姬无命", "value":"仇人", "symbol":["arrow",""]},
    {"source": "吕轻侯", "target": "郭芙蓉", "value":"情侣", "symbol":["arrow",""]},
    {"source": "姬无命", "target": "吕轻侯", "value":"仇人", "symbol":["arrow",""]},
    {"source": "姬无命", "target": "白展堂", "value":"昔日好友", "symbol":["arrow",""]},
    {"source": "姬无命", "target": "公孙乌龙", "value":"徒弟", "symbol":["arrow",""]},
    {"source": "祝无双", "target": "白展堂", "value":"师妹", "symbol":["arrow",""]},
    {"source": "祝无双", "target": "燕小六", "value":"情侣", "symbol":["arrow",""]},
    {"source": "燕小六", "target": "祝无双", "value":"情侣", "symbol":["arrow",""]},
    {"source": "燕小六", "target": "邢育森", "value":"徒弟", "symbol":["arrow",""]},
    {"source": "李秀莲", "target": "佟湘玉", "value":"佣人", "symbol":["arrow",""]},
    {"source": "李秀莲", "target": "杨蕙兰", "value":"单恋", "symbol":["arrow",""]},
    {"source": "李秀莲", "target": "断指轩辕", "value":"儿子", "symbol":["arrow",""]},
    {"source": "赛貂蝉", "target": "小翠", "value":"主人", "symbol":["arrow",""]},
    {"source": "小翠", "target": "赛貂蝉", "value":"仆人", "symbol":["arrow",""]},
    {"source": "小青", "target": "郭芙蓉", "value":"仆人", "symbol":["arrow",""]},
]

# 创建图表对象，进行链式调用
graph = (
    Graph(init_opts=opts.InitOpts(width='100%'))
    .set_global_opts(
        title_opts=opts.TitleOpts(title="武林外传人物关系图",pos_left="center"),
        tooltip_opts=opts.TooltipOpts(formatter="{b}: {c}"),
        legend_opts=opts.LegendOpts(pos_top="10%",pos_right="10%",)
    )
    .add(
        "",
        nodes,
        links,
        categories=[{"name": "主角"},{"name":"配角"}],
        layout="force",
        repulsion=1000,
        is_draggable=True,
        is_focusnode=True,
        linestyle_opts=opts.LineStyleOpts(width=1.5, curve=0),
        edge_label=opts.LabelOpts(
            is_show=True, position="middle", formatter="{c}"
        ),
    )
    .set_series_opts(
        tooltip_opts=opts.TooltipOpts(
            formatter=JsCode(
                """function(params) {
                    if ('info' in params.data) {
                        return params.data.info;
                    }
                    else {
                        return params.name;
                    }
                }"""
            ),
        ),
        label_opts=opts.LabelOpts(
            position="bottom",
        ),
    )
)

# 渲染图表并保存到文件
graph.render("demo.html")
# graph.render_notebook()
```

### 最终效果
> 有个小Bug，markdown中嵌入关系图，人物头像不显示，还在定位问题，后续尝试修复。
{: .prompt-danger }
> 
<html><head>
    <meta charset="UTF-8">
    <title>Awesome-pyecharts</title>
                <script type="text/javascript" src="https://assets.pyecharts.org/assets/v5/echarts.min.js"></script>

</head>
<body>
    <div id="f18c219426c541dcb737ef3ae1540dce" class="chart-container" style="width: 100%; height: 500px; user-select: none; -webkit-tap-highlight-color: rgba(0, 0, 0, 0); position: relative;" _echarts_instance_="ec_1687058797649"><div style="position: relative; width: 1675px; height: 500px; padding: 0px; margin: 0px; border-width: 0px; cursor: default;"><canvas data-zr-dom-id="zr_0" width="2512" height="750" style="position: absolute; left: 0px; top: 0px; width: 1675px; height: 500px; user-select: none; -webkit-tap-highlight-color: rgba(0, 0, 0, 0); padding: 0px; margin: 0px; border-width: 0px;"></canvas></div><div class="" style="position: absolute; display: block; border-style: solid; white-space: nowrap; z-index: 9999999; box-shadow: rgba(0, 0, 0, 0.2) 1px 2px 10px; background-color: rgb(255, 255, 255); border-width: 0px; border-radius: 4px; color: rgb(102, 102, 102); font: 14px / 21px &quot;Microsoft YaHei&quot;; padding: 5px; top: 0px; left: 0px; transform: translate3d(1014px, 46px, 0px); border-color: rgb(145, 204, 117); pointer-events: none; visibility: hidden; opacity: 0;">姓名：断指轩辕<br>职业：千堵之王<br>称号：断指<br>武器：出老千<br>名言：我吃的盐比你吃的米还多呢！<br>演员：张少华<br>特点：教子有方</div></div>
    <script>
        var chart_f18c219426c541dcb737ef3ae1540dce = echarts.init(
            document.getElementById('f18c219426c541dcb737ef3ae1540dce'), 'white', {renderer: 'canvas'});
            

    
    
        var option_f18c219426c541dcb737ef3ae1540dce = {
    "animation": true,
    "animationThreshold": 2000,
    "animationDuration": 1000,
    "animationEasing": "cubicOut",
    "animationDelay": 0,
    "animationDurationUpdate": 300,
    "animationEasingUpdate": "cubicOut",
    "animationDelayUpdate": 0,
    "aria": {
        "enabled": false
    },
    "color": [
        "#5470c6",
        "#91cc75",
        "#fac858",
        "#ee6666",
        "#73c0de",
        "#3ba272",
        "#fc8452",
        "#9a60b4",
        "#ea7ccc"
    ],
    "series": [
        {
            "type": "graph",
            "layout": "force",
            "symbolSize": 10,
            "circular": {
                "rotateLabel": false
            },
            "force": {
                "repulsion": 1000,
                "gravity": 0.2,
                "edgeLength": 30,
                "friction": 0.6,
                "layoutAnimation": true
            },
            "label": {
                "show": true,
                "position": "bottom",
                "margin": 8
            },
            "lineStyle": {
                "show": true,
                "width": 1.5,
                "opacity": 1,
                "curveness": 0,
                "type": "solid"
            },
            "roam": true,
            "draggable": true,
            "focusNodeAdjacency": true,
            "data": [
                {
                    "name": "\u4f5f\u6e58\u7389",
                    "symbol": "path:///assets/images/demo.jpg",
                    "category": 0,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u4f5f\u6e58\u7389<br>\u804c\u4e1a\uff1a\u540c\u798f\u5ba2\u6808\u638c\u67dc<br>\u79f0\u53f7\uff1a\u638c\u67dc\u7684<br>\u6b66\u5668\uff1a\u70fd\u706b\u9739\u96f3\u5f39<br>\u540d\u8a00\uff1a\u6211\u6ef4\u795e\u5440\uff0c\u4e0a\u5e1d\u4ee5\u53ca\u8001\u5929\u7237\u5440\uff01<br>\u6f14\u5458\uff1a\u95eb\u59ae<br>\u7279\u70b9\uff1a\u62a0\u95e8\uff0c\u5584\u89e3\u4eba\u610f\uff0c\u660e\u4e8b\u7406"
                },
                {
                    "name": "\u767d\u5c55\u5802",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/smart/aa64034f78f0f73639182abf0455b319eac413ad-bkimg-process",
                    "category": 0,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u767d\u5c55\u5802<br>\u804c\u4e1a\uff1a\u540c\u798f\u5ba2\u6808\u8dd1\u5802<br>\u79f0\u53f7\uff1a\u76d7\u5723<br>\u6b66\u5668\uff1a\u8475\u82b1\u70b9\u7a74\u624b<br>\u540d\u8a00\uff1a\u624b\u91cc\u6367\u7740\u7a9d\u7a9d\u5934\uff0c\u83dc\u91cc\u6ca1\u6709\u4e00\u6ef4\u6cb9\u2026\u2026<br>\u6f14\u5458\uff1a\u6c99\u6ea2<br>\u7279\u70b9\uff1a\u6027\u5b50\u723d\u6717\uff0c\u660e\u767d\u4e8b\u7406\uff0c\u6709\u8d23\u4efb\u5fc3\uff0c\u80c6\u5c0f"
                },
                {
                    "name": "\u674e\u79c0\u83b2",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/smart/7a899e510fb30f2484c3ce96c295d143ac4b03cd-bkimg-process",
                    "category": 0,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u674e\u79c0\u83b2<br>\u804c\u4e1a\uff1a\u540c\u798f\u5ba2\u6808\u53a8\u5e08<br>\u79f0\u53f7\uff1a\u674e\u5927\u5634<br>\u6b66\u5668\uff1a\u7384\u94c1\u83dc\u5200<br>\u540d\u8a00\uff1a\u5144\u5f1f\u4f60\u752d\u8bf4\u4e86\uff0c\u8fd9\u4e8b\u513f\u5305\u6211\u8eab\u4e0a\u4e86\u3002<br>\u6f14\u5458\uff1a\u59dc\u8d85<br>\u7279\u70b9\uff1a\u6d41\u6c13\u5047\u4ed7\u4e49\uff0c\u5047\u52c7\u5047\u9c81\uff0c\u4e00\u5fc3\u60f3\u5b66\u6b66\u529f\u3001\u603b\u60f3\u884c\u4fa0\u4ed7\u4e49\uff0c\u53ea\u8981\u4e00\u51fa\u624b\u5c31\u5fc5\u662f\u60f9\u7978"
                },
                {
                    "name": "\u90ed\u8299\u84c9",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/smart/8c1001e93901213fb80ef0e98db621d12f2eb9383ffe-bkimg-process",
                    "category": 0,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u90ed\u8299\u84c9<br>\u804c\u4e1a\uff1a\u540c\u798f\u5ba2\u6808\u6742\u5f79<br>\u79f0\u53f7\uff1a\u8299\u59b9<br>\u6b66\u5668\uff1a\u6392\u5c71\u5012\u6d77<br>\u540d\u8a00\uff1a\u786e\u5b9a\u4e00\u5b9a\u4ee5\u53ca\u80af\u5b9a\u3002<br>\u6f14\u5458\uff1a\u59da\u6668<br>\u7279\u70b9\uff1a\u76f4\u723d\uff0c\u6562\u7231\u6562\u6068\uff0c\u4e0d\u8ba1\u524d\u5acc\uff0c\u5201\u86ee\uff0c\u61d2\u60f0\uff0c\u6709\u65f6\u5a07\u6c14\uff0c\u4e71\u82b1\u94b1\uff0c\u7231\u4f5c\u68a6\uff0c\u8111\u5b50\u4e00\u6839\u7b4b\uff0c\u7ecf\u5e38\u4e0a\u5f53\u53d7\u9a97"
                },
                {
                    "name": "\u5415\u8f7b\u4faf",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/smart/0dd7912397dda144c0b0a361b7b7d0a20df486ac-bkimg-process",
                    "category": 0,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u5415\u8f7b\u4faf<br>\u804c\u4e1a\uff1a\u540c\u798f\u5ba2\u6808\u8d26\u623f<br>\u79f0\u53f7\uff1a\u79c0\u624d<br>\u6b66\u5668\uff1a\u77e5\u8bc6<br>\u540d\u8a00\uff1a\u5b50\u66fe\u7ecf\u66f0\u8fc7\u2026\u2026<br>\u6f14\u5458\uff1a\u55bb\u6069\u6cf0<br>\u7279\u70b9\uff1a\u88ab\u6b3a\u8d1f\u3001\u5403\u918b\u3001\u7b97\u5e10\u3001\u62fd\u6587\u3001\u5199\u8bd7\u3001\u6350\u6b3e\u3001\u7ebf\u6027\u4ee3\u6570\u3001\u5fae\u79ef\u5206\u3001\u9ad8\u7b49\u7269\u7406\u3001\u7cbe\u7ec6\u5316\u5de5\u3001\u6d0b\u6587\u3001\u77e5\u8bc6\u95ee\u7b54 \u3002"
                },
                {
                    "name": "\u90a2\u80b2\u68ee",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/smart/622762d0f703918ffbedc1125b3d269759eec42e-bkimg-process",
                    "category": 1,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u90a2\u80b2\u68ee<br>\u804c\u4e1a\uff1a\u4e03\u4fa0\u954737\u4efb\u7f01\u8863\u6355\u5934<br>\u79f0\u53f7\uff1a\u8001\u90a2<br>\u6b66\u5668\uff1a\u6355\u5934\u4f69\u5200<br>\u540d\u8a00\uff1a\u6211\u770b\u597d\u4f60\u54df\u3002\u4eb2\u5a18\u561e\uff01<br>\u6f14\u5458\uff1a\u8303\u660e<br>\u7279\u70b9\uff1a\u5de1\u8857\u3001\u8e6d\u5403\u8e6d\u559d\uff0c\u5403\u4eba\u5634\u4e0d\u8f6f\uff0c\u62ff\u4eba\u624b\u4e0d\u77ed"
                },
                {
                    "name": "\u71d5\u5c0f\u516d",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/pic/72f082025aafa40fa57e050eae64034f79f019ad?x-bce-process",
                    "category": 1,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u71d5\u5c0f\u516d<br>\u804c\u4e1a\uff1a\u4e03\u4fa0\u954738\u4efb\u7f01\u8863\u6355\u5934<br>\u79f0\u53f7\uff1a\u5c0f\u516d<br>\u6b66\u5668\uff1a\u8131\u978b<br>\u540d\u8a00\uff1a\u5e2e\u6211\u7167\u987e\u597d\u6211\u4e03\u8205\u59e5\u7237\u548c\u4ed6\u4e09\u5916\u7525\u5973!<br>\u6f14\u5458\uff1a\u8096\u5251<br>\u7279\u70b9\uff1a\u5934\u8111\u7b80\u5355\uff0c\u4f46\u662f\u5fc3\u80a0\u70ed\u3001\u88c5\u5b98\u8154\u3001\u53cc\u624b\u62b1\u62f3\u606d\u7ef4\u3001\u6253\u5929\u6d25\u5feb\u677f\u3001\u5522\u5450\u3001\u4e8c\u80e1"
                },
                {
                    "name": "\u795d\u65e0\u53cc",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/smart/b21c8701a18b87d62ec299cb020828381e30fd65-bkimg-process",
                    "category": 1,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u795d\u65e0\u53cc<br>\u804c\u4e1a\uff1a\u4e03\u4fa0\u9547\u552f\u4e00\u5973\u6355\u5feb<br>\u79f0\u53f7\uff1a\u8d85\u7ea7\u6028\u5987<br>\u6b66\u5668\uff1a\u8475\u82b1\u70b9\u7a74\u624b<br>\u540d\u8a00\uff1a\u653e\u7740\u6211\u6765\uff01<br>\u6f14\u5458\uff1a\u502a\u8679\u6d01<br>\u7279\u70b9\uff1a\u6e29\u67d4\u8d24\u60e0\u3001\u4f53\u8d34\u5165\u5fae\u3001\u5229\u843d\u4ed4\u7ec6\u3001\u6709\u7231\u5fc3\u540c\u60c5\u5fc3\u3001\u660e\u4e8b\u7406"
                },
                {
                    "name": "\u767d\u7fe0\u840d",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/smart/86d6277f9e2f070839091dd4ec24b899a801f2d1-bkimg-process",
                    "category": 1,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u767d\u7fe0\u840d<br>\u804c\u4e1a\uff1a\u516d\u6247\u95e8\u5bc6\u4f7f<br>\u79f0\u53f7\uff1a\u767d\u4e09\u5a18<br>\u6b66\u5668\uff1a\u8475\u82b1\u70b9\u7a74\u624b<br>\u540d\u8a00\uff1a\u65e0<br>\u6f14\u5458\uff1a\u9ec4\u6653\u5a1f<br>\u7279\u70b9\uff1a\u5bf9\u4eb2\u4eba\u5982\u6625\u5929\u822c\u6e29\u6696\uff0c\u5bf9\u654c\u4eba\u5982\u51ac\u5929\u822c\u51b7\u9177\u65e0\u60c5\uff0c\u591a\u7591\uff0c\u51b7\u9759\u3002\u66fe\u8650\u5f85\u4f5f\u6e58\u7389\u4e00\u5929\u591a\u3002"
                },
                {
                    "name": "\u516c\u5b59\u4e4c\u9f99",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/smart/0b55b319ebc4b74543a9e9e2b6aa09178a82b801bfb3-bkimg-process",
                    "category": 1,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u516c\u5b59\u4e4c\u9f99<br>\u804c\u4e1a\uff1a\u7edd\u4e16\u9ad8\u624b<br>\u79f0\u53f7\uff1a\u7edd\u4e16\u9ad8\u624b<br>\u6b66\u5668\uff1a\u4f20\u97f3\u5165\u5bc6<br>\u540d\u8a00\uff1a\u5584\u54c9\uff0c\u5584\u54c9\uff01<br>\u6f14\u5458\uff1a\u767d\u5fd7\u8fea<br>\u7279\u70b9\uff1a\u5fc3\u72e0\u624b\u8fa3"
                },
                {
                    "name": "\u8d5b\u8c82\u8749",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/smart/0dd7912397dda144f1a15f3eb8b7d0a20df48695-bkimg-process",
                    "category": 1,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u8d5b\u8c82\u8749<br>\u804c\u4e1a\uff1a\u6021\u7ea2\u697c\u638c\u67dc<br>\u79f0\u53f7\uff1a\u8d5b\u638c\u67dc<br>\u6b66\u5668\uff1a\u5077\u7a0e\u6f0f\u7a0e<br>\u540d\u8a00\uff1a\u65e0<br>\u6f14\u5458\uff1a\u5218\u654f<br>\u7279\u70b9\uff1a\u8d2a\u5a6a\uff0c\u65e0\u803b\uff0c\u5de5\u4e8e\u5fc3\u8ba1\uff0c\u7ecf\u4f5f\u6e58\u7389\u4e0d\u8ba1\u524d\u5acc\u613f\u4e3a\u5176\u8d4e\u8eab\u4e00\u4e8b\u540e\u6d17\u5fc3\u9769\u9762\u5f03\u6076\u4ece\u5584"
                },
                {
                    "name": "\u59ec\u65e0\u547d",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/smart/6a63f6246b600c33537d9e671a4c510fd9f9a11d-bkimg-process",
                    "category": 1,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u59ec\u65e0\u547d<br>\u804c\u4e1a\uff1a\u6c5f\u6e56\u4eba\u58eb<br>\u79f0\u53f7\uff1a\u76d7\u795e<br>\u6b66\u5668\uff1a\u4e0d\u8be6<br>\u540d\u8a00\uff1a\u662f\u6211\u6740\u4e86\u6211\uff01<br>\u6f14\u5458\uff1a\u738b\u78ca<br>\u7279\u70b9\uff1a\u5fc3\u72e0\u624b\u8fa3"
                },
                {
                    "name": "\u83ab\u5c0f\u8d1d",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/smart/bd3eb13533fa828ba61ec80bca4f5634970a314eec81-bkimg-process",
                    "category": 0,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u83ab\u5c0f\u8d1d<br>\u804c\u4e1a\uff1a\u8861\u5c71\u6d3e\u638c\u95e8<br>\u79f0\u53f7\uff1a\u8d64\u7130\u72c2\u9b54<br>\u6b66\u5668\uff1a\u9694\u7a7a\u6253\u7a74<br>\u540d\u8a00\uff1a\u5ac2\u5b50\u2026\u4ed6\u4eec\u6b3a\u8d1f\u6211\u4e86\u5566\u2026\u2026<br>\u6f14\u5458\uff1a\u738b\u838e\u838e<br>\u7279\u70b9\uff1a\u53e4\u7075\u7cbe\u602a\u3001\u5e7d\u9ed8\u800d\u5b9d\u3001\u4e0d\u7231\u5b66\u4e60\u7231\u62cc\u5634\u3001\u72ec\u7acb\u81ea\u4e3b"
                },
                {
                    "name": "\u6768\u8559\u5170",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/pic/2934349b033b5bb5c9ea7032ee82c239b6003bf316e7?x-bce-process",
                    "category": 1,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u6768\u8559\u5170<br>\u804c\u4e1a\uff1a\u6c5f\u6e56\u4eba\u58eb<br>\u79f0\u53f7\uff1a\u60e0\u5170<br>\u6b66\u5668\uff1a\u5be1\u5987\u5200<br>\u540d\u8a00\uff1a\u65e0<br>\u6f14\u5458\uff1a\u4e8e\u5a1f<br>\u7279\u70b9\uff1a\u559c\u6b22\u94b1\uff0c\u4e2a\u6027\u51f6\u6b8b\uff0c\u7231\u559d\u9152\u3001\u5565\u90fd\u8981\u5c31\u662f\u4e0d\u8981\u5927\u5634\u3002"
                },
                {
                    "name": "\u65ad\u6307\u8f69\u8f95",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/pic/55e736d12f2eb938a0457106df628535e5dd6f1d?x-bce-process",
                    "category": 1,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u65ad\u6307\u8f69\u8f95<br>\u804c\u4e1a\uff1a\u5343\u5835\u4e4b\u738b<br>\u79f0\u53f7\uff1a\u65ad\u6307<br>\u6b66\u5668\uff1a\u51fa\u8001\u5343<br>\u540d\u8a00\uff1a\u6211\u5403\u7684\u76d0\u6bd4\u4f60\u5403\u7684\u7c73\u8fd8\u591a\u5462\uff01<br>\u6f14\u5458\uff1a\u5f20\u5c11\u534e<br>\u7279\u70b9\uff1a\u6559\u5b50\u6709\u65b9"
                },
                {
                    "name": "\u5c0f\u9752",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/smart/faedab64034f78f047a8ee2a7c310a55b2191c43-bkimg-process",
                    "category": 1,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u5c0f\u9752<br>\u804c\u4e1a\uff1a\u90ed\u8299\u84c9\u4e2b\u73af<br>\u79f0\u53f7\uff1a\u96cc\u96c4\u53cc\u715e<br>\u6b66\u5668\uff1a\u5251<br>\u540d\u8a00\uff1a\u65e0<br>\u6f14\u5458\uff1a\u5f20\u6b46\u827a<br>\u7279\u70b9\uff1a\u5bf9\u5c0f\u59d0\u5fe0\u5fc3"
                },
                {
                    "name": "\u5c0f\u7fe0",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/smart/8c1001e93901213fc8de730851e736d12e2e9570-bkimg-process",
                    "category": 1,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u5c0f\u7fe0<br>\u804c\u4e1a\uff1a\u8d5b\u8c82\u8749\u4e2b\u73af<br>\u79f0\u53f7\uff1a\u65e0<br>\u6b66\u5668\uff1a\u590d\u8bfb\u673a<br>\u540d\u8a00\uff1a\u91cd\u590d\u8d5b\u8c82\u8749\u8bf4\u7684\u8bdd\u7684\u540e\u9762\u51e0\u4e2a\u5b57\uff08\u50cf\u4e2a\u56de\u97f3\u97f3\u54cd\uff09<br>\u6f14\u5458\uff1a\u848b\u5349<br>\u7279\u70b9\uff1a\u70ed\u60c5\u3001\u5014\u5f3a\u3001\u4e0d\u670d\u8f93\u3001\u672c\u6027\u6df3\u6734\u5584\u826f\uff08\u8d5b\u8c82\u8749\u8bed\uff09\uff0c\u8bb0\u4ec7"
                },
                {
                    "name": "\u5c55\u7ea2\u7eeb",
                    "symbol": "image://https://bkimg.cdn.bcebos.com/pic/d31b0ef41bd5ad6eddc462820b9d2edbb6fd52669607?x-bce-process",
                    "category": 1,
                    "label": {
                        "show": true,
                        "color": "#000",
                        "margin": 8,
                        "fontWeight": "bold",
                        "formatter": "{b}\n\u540c\u798f\u5ba2\u6808\u638c\u67dc"
                    },
                    "info": "\u59d3\u540d\uff1a\u5c55\u7ea2\u7eeb<br>\u804c\u4e1a\uff1a\u516d\u6247\u95e8\u6355\u5934<br>\u79f0\u53f7\uff1a\u7ea2\u7eeb<br>\u6b66\u5668\uff1a\u5224\u5b98\u593a\u547d\u7b14<br>\u540d\u8a00\uff1a\u5973\u4eba\u7684\u76f4\u89c9<br>\u6f14\u5458\uff1a\u970d\u66fc\u8fea<br>\u7279\u70b9\uff1a\u6293\u8d3c\u3001\u8ffd\u8d3c"
                }
            ],
            "categories": [
                {
                    "name": "\u4e3b\u89d2"
                },
                {
                    "name": "\u914d\u89d2"
                }
            ],
            "edgeLabel": {
                "show": true,
                "position": "middle",
                "margin": 8,
                "formatter": "{c}"
            },
            "edgeSymbol": [
                null,
                null
            ],
            "edgeSymbolSize": 10,
            "links": [
                {
                    "source": "\u4f5f\u6e58\u7389",
                    "target": "\u767d\u5c55\u5802",
                    "value": "\u60c5\u4fa3",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u4f5f\u6e58\u7389",
                    "target": "\u674e\u79c0\u83b2",
                    "value": "\u96c7\u4e3b",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u4f5f\u6e58\u7389",
                    "target": "\u90ed\u8299\u84c9",
                    "value": "\u96c7\u4e3b",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u4f5f\u6e58\u7389",
                    "target": "\u5415\u8f7b\u4faf",
                    "value": "\u96c7\u4e3b",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u4f5f\u6e58\u7389",
                    "target": "\u83ab\u5c0f\u8d1d",
                    "value": "\u5ac2\u5b50",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u4f5f\u6e58\u7389",
                    "target": "\u8d5b\u8c82\u8749",
                    "value": "\u5bf9\u624b",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u767d\u5c55\u5802",
                    "target": "\u4f5f\u6e58\u7389",
                    "value": "\u60c5\u4fa3",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u767d\u5c55\u5802",
                    "target": "\u795d\u65e0\u53cc",
                    "value": "\u5e08\u5144",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u767d\u5c55\u5802",
                    "target": "\u59ec\u65e0\u547d",
                    "value": "\u6614\u65e5\u597d\u53cb",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u767d\u5c55\u5802",
                    "target": "\u5c55\u7ea2\u7eeb",
                    "value": "\u53cb\u4eba",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u767d\u5c55\u5802",
                    "target": "\u767d\u7fe0\u840d",
                    "value": "\u513f\u5b50",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u90ed\u8299\u84c9",
                    "target": "\u5415\u8f7b\u4faf",
                    "value": "\u60c5\u4fa3",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u90ed\u8299\u84c9",
                    "target": "\u4f5f\u6e58\u7389",
                    "value": "\u4f63\u4eba",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u90ed\u8299\u84c9",
                    "target": "\u5c0f\u9752",
                    "value": "\u4e3b\u4eba",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u5415\u8f7b\u4faf",
                    "target": "\u4f5f\u6e58\u7389",
                    "value": "\u4f63\u4eba",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u5415\u8f7b\u4faf",
                    "target": "\u59ec\u65e0\u547d",
                    "value": "\u4ec7\u4eba",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u5415\u8f7b\u4faf",
                    "target": "\u90ed\u8299\u84c9",
                    "value": "\u60c5\u4fa3",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u59ec\u65e0\u547d",
                    "target": "\u5415\u8f7b\u4faf",
                    "value": "\u4ec7\u4eba",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u59ec\u65e0\u547d",
                    "target": "\u767d\u5c55\u5802",
                    "value": "\u6614\u65e5\u597d\u53cb",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u59ec\u65e0\u547d",
                    "target": "\u516c\u5b59\u4e4c\u9f99",
                    "value": "\u5f92\u5f1f",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u795d\u65e0\u53cc",
                    "target": "\u767d\u5c55\u5802",
                    "value": "\u5e08\u59b9",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u795d\u65e0\u53cc",
                    "target": "\u71d5\u5c0f\u516d",
                    "value": "\u60c5\u4fa3",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u71d5\u5c0f\u516d",
                    "target": "\u795d\u65e0\u53cc",
                    "value": "\u60c5\u4fa3",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u71d5\u5c0f\u516d",
                    "target": "\u90a2\u80b2\u68ee",
                    "value": "\u5f92\u5f1f",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u674e\u79c0\u83b2",
                    "target": "\u4f5f\u6e58\u7389",
                    "value": "\u4f63\u4eba",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u674e\u79c0\u83b2",
                    "target": "\u6768\u8559\u5170",
                    "value": "\u5355\u604b",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u674e\u79c0\u83b2",
                    "target": "\u65ad\u6307\u8f69\u8f95",
                    "value": "\u513f\u5b50",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u8d5b\u8c82\u8749",
                    "target": "\u5c0f\u7fe0",
                    "value": "\u4e3b\u4eba",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u5c0f\u7fe0",
                    "target": "\u8d5b\u8c82\u8749",
                    "value": "\u4ec6\u4eba",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                },
                {
                    "source": "\u5c0f\u9752",
                    "target": "\u90ed\u8299\u84c9",
                    "value": "\u4ec6\u4eba",
                    "symbol": [
                        "arrow",
                        ""
                    ]
                }
            ],
            "tooltip": {
                "show": true,
                "trigger": "item",
                "triggerOn": "mousemove|click",
                "axisPointer": {
                    "type": "line"
                },
                "showContent": true,
                "alwaysShowContent": false,
                "showDelay": 0,
                "hideDelay": 100,
                "enterable": false,
                "confine": false,
                "appendToBody": false,
                "transitionDuration": 0.4,
                "formatter": function(params) {                    if ('info' in params.data) {                        return params.data.info;                    }                    else {                        return params.name;                    }                },
                "textStyle": {
                    "fontSize": 14
                },
                "borderWidth": 0,
                "padding": 5,
                "order": "seriesAsc"
            },
            "rippleEffect": {
                "show": true,
                "brushType": "stroke",
                "scale": 2.5,
                "period": 4
            }
        }
    ],
    "legend": [
        {
            "data": [
                "\u4e3b\u89d2",
                "\u914d\u89d2"
            ],
            "selected": {},
            "show": true,
            "right": "10%",
            "top": "10%",
            "padding": 5,
            "itemGap": 10,
            "itemWidth": 25,
            "itemHeight": 14,
            "backgroundColor": "transparent",
            "borderColor": "#ccc",
            "borderWidth": 1,
            "borderRadius": 0,
            "pageButtonItemGap": 5,
            "pageButtonPosition": "end",
            "pageFormatter": "{current}/{total}",
            "pageIconColor": "#2f4554",
            "pageIconInactiveColor": "#aaa",
            "pageIconSize": 15,
            "animationDurationUpdate": 800,
            "selector": false,
            "selectorPosition": "auto",
            "selectorItemGap": 7,
            "selectorButtonGap": 10
        }
    ],
    "tooltip": {
        "show": true,
        "trigger": "item",
        "triggerOn": "mousemove|click",
        "axisPointer": {
            "type": "line"
        },
        "showContent": true,
        "alwaysShowContent": false,
        "showDelay": 0,
        "hideDelay": 100,
        "enterable": false,
        "confine": false,
        "appendToBody": false,
        "transitionDuration": 0.4,
        "formatter": "{b}: {c}",
        "textStyle": {
            "fontSize": 14
        },
        "borderWidth": 0,
        "padding": 5,
        "order": "seriesAsc"
    },
    "title": [
        {
            "show": true,
            "text": "\u6b66\u6797\u5916\u4f20\u4eba\u7269\u5173\u7cfb\u56fe",
            "target": "blank",
            "subtarget": "blank",
            "left": "center",
            "padding": 5,
            "itemGap": 10,
            "textAlign": "auto",
            "textVerticalAlign": "auto",
            "triggerEvent": false
        }
    ]
};
        chart_f18c219426c541dcb737ef3ae1540dce.setOption(option_f18c219426c541dcb737ef3ae1540dce);
            window.addEventListener('resize', function(){
                chart_f18c219426c541dcb737ef3ae1540dce.resize();
            })
    </script>


</body></html>

## 后续优化

折腾了好久，总算是弄出来了，但还是有许多需要优化的地方，以后有时间再慢慢优化吧。
1. 主角、配角图例添加自定义图片；
2. 添加JsCode，使人物头像以圆形展示；
3. 人物关系之间连线显示优化；
4. 整体显示效果优化，如字体、颜色等；
5. Bug修复：解决markdown中嵌入关系图，人物头像不显示问题；
6. 代码优化：nodes信息和links信息通过json文件读取，减少代码量。
