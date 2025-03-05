#  问题日志

## 1.如何构建属于自己项目的提示词

- 如果是从0开始开发，则先选择技术类型，然后使用claude 3.7-sonnet 编写提示词；

>我准备开发XXX项目，我的技术选型是：
>
>1.前端：XXX
>
>2.后端：XXX
>
>请你根据我项目和技术选型编写出最佳项目提示词；

- 如果是再已有的项目上进行开发，则在cursor编辑器中写：

step1：请先浏览我的项目，做下介绍；

step2：根据项目介绍，为我编写出最佳项目提示词；



	>我的一些认为好的rules：
	>
	>1. 在项目规则中要求创建项目结构树，变更日志文档；要求Agent在每次做出重大更新时，更新文档；
	>2. 根据网上的建议：json格式比MarkDown格式的提示词更好；
	>
	>



## 2.如何创建前后端项目

截至2025/3/4为止，像==claude这样的gpt==可以编写出优秀的前端页面，所以难点不在前端页面；而在于后端；

而后端需要依靠API接口；

因此需要先找到前端中哪些数据可以保存到后端中(可以使用),然后让AI编写一个API接口与数据库表；

然后根据前端的API接口文档与数据库表来构造后端；







## Cusor续杯

MCP在cursor编辑器中一直报错；

>cursor续杯问题：
>
>在power中执行脚本：
>
>irm https://aizaozao.com/accelerate.php/https://raw.githubusercontent.com/yuaotian/go-cursor-help/refs/heads/master/scripts/run/cursor_win_id_modifier.ps1 | iex
>
>

