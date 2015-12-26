title: 一个简单的B/S开发流程
tags:
  - B/S
  - 开发
  - 项目
id: 642
categories:
  - 工作记录
date: 2010-07-29 10:31:27
---

<span style="color: #ff0000;">1.BD阶段（bussiness develop） </span>

具体的不说了。主要是要根据客户的大概的一个需求，替客户制定出系统构架的建议。
主要包含采用　什么样的技术手段，采用什么样的服务器，什么样的系统结构等等。
产生的文档应该叫系统的整体设计吧。（Proposal）
<span style="color: #ff0000;">2.功能分析（function analyse） </span>

与客户进行具体功能和流程的分析和设计，确定功能。
产生的文档：功能说明书Function Spec（B/S结构的系统，一般有做好的整个系统的
静态网页作为DEMO）　此文档需要客户签字认可。
<span style="color: #ff0000;">3.项目进程安排与分工计划。(project plan)</span>

这是正式开始项目的第一步工作，安排项目进度。列出项目进度表和分工表。（这个进程表要按项目的实际进程不断修改和完善）
产生文档：项目进度表
<span style="color: #ff0000;">4.技术设计阶段(technical design)</span>

主要是从技术角度设计系统，完成系统技术方面的设计和系统整体编码构架的计划。
制定开发规则，编码规则等。
产生文档：技术设计说明书(Technical design spec)
<span style="color: #ff0000;">5.编码设计(program design) </span>

根据功能制定编码流程，结构层次和各个接口。
产生文档：编码说明书（Program spec）

<!--more-->
<span style="color: #ff0000;">6.编码(coding)</span>

进行模块分工，根据编码说明和功能说明进行编码
完成的东东：模块代码+代码内的注释说明

<span style="color: #ff0000;">7.单元测试(unit test)</span>

对完成的单个模块进行测试。
产生文档：单元测试报告

<span style="color: #ff0000;">8.系统集成测试(system integerity test)</span>

将通过单元测试的整个系统整和在一起作为一个整体进行测试
产生文档：系统测试报告

<span style="color: #ff0000;">9.用户测试(user acceptance test)</span>

将系统交给用户试用
需要准备的文档：错误报告表

<span style="color: #ff0000;">10.实施(implementation)</span>

完整的替客户安装系统
需要准备的文档：系统实施计划

<span style="color: #ff0000;">11.质保期(warranty)</span>