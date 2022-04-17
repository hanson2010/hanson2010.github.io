---
title: 《The Art of Lean Software Development》读书笔记
date: 2010-03-29T22:59:28+08:00
categories:
- Life
tags:
- lean
- agile
- scrum
---

Lean从丰田生产系统发展而来，首先是几个常见的日文字：

* **Andon** - Means “light” in Japanese. In a Lean environment, it is a visual device (usually a light or a board of lights) that gives the current status of a production system, signaling any problems (typically, green = OK, yellow = needs attention, and red = urgent/production stopped).
* **Jidoka** - Autonomation, the ability of a machine to inspect its work and operation and to notify a human if a problem is detected.
* **Kaizen** - The continuous, incremental improvement of an activity to create more value with less waste.
* **Kanban** - A signaling system used to signal the need for an item, typically using things like index cards, colored golf balls, or empty carts.
* **Muda** - Waste that consumes resources but produces no value.
<!-- more -->
Lean软件开发的七个原则：

* Eliminate waste
* Build quality in
* Create knowledge
* Defer commitment
* Deliver fast
* Respect people
* Optimize the whole

比较Agile软件开发和Lean软件开发的不同：

|     | Agile | Lean |
| --- | ----- | ---- |
| 目光 | 软件开发实践和项目管理 | 任何范围，可能延伸至整个企业；<br>Lean把Agile视为一种可行的支持性实践 |
| 聚焦 | 客户协作和快速交付 | 从客户的角度消除浪费（Muda）；<br>消除浪费的一个主要工具是Value Stream Mapping (VSM) |
| 包装 | 有正式方法论 | 只有一些推荐实践 |
| 操作 |  | 从Agile（例如Scrum）开始，然后加上VSM |

Lean软件开发实践之concrete practices

* Source Code Management and Scripted Builds
* Automated Testing
* Continuous Integration
* Less Code
* Short Iterations
* Customer Participation

Lean软件开发实践之analysis practices

* Kaizen (continuous improvement)
* Kaizen Workshops
* Value Stream Mapping (VSM): value-added, non-value-added, or non-value-added but necessary
* Root Cause Analysis (five whys)
* Kanban
