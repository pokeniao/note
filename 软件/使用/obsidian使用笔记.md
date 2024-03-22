---
日期: 2024-03-17
aliases:
  - 这里是别名
tags:
  - 软件使用
---

# 添加元数据（文档属性）
作用：方便后续搜索
使用： 在笔记头写上 ---


# Markdown语言编写

## 分级标题
使用：# 一级 ## 二级 等。。。 
## 添加链接
- 作用：可以链接到其他的笔记,或者网站
- 使用：
	1. 链接名普通使用：`[[` 链接笔记 `]]`
	2. 链接名重命名：`[[` 链接标题|链接名 `]]`
	3. 链接到标题：`[[` 链接标题#标签名 `]]`
	4. 链接到具体内容：`[[` 链接标题^内容位置（一串内容的地址）`]]
	5. 链接嵌入
		1. 介绍：将链接到的内容直接展示出来
		2. 使用：直接在链接的基础上在前面加上 `!` 号 如：！`[[` 链接标题|链接名 `]]`
	6. 外部链接
		1. 介绍：链接到网站
		2. 使用：`[` 名字 `]` (https://)
- 其他概念：
	反向链接：可以看到谁链接到本笔记

## 文字
1. 加粗： `**加粗内容**`  比如 **你好**
2. 斜体：`*斜体内容*` 或者 `_斜体_` 比如*你好* _斜体_
3. 高亮： `==高亮内容==` 比如 ==高亮内容==
4. 任务： - [ ]任务1
	- [ ] 任务
5. 列表
	1. 我是有序列表使用 `1.空格`
	- 我是无须列表 `-空格`
6. 引用：`>空格`
	>我是引用
	>>我是引用
7. 标注：`>[!NOTE] 我是标注` `>[!danger] 我是标注` 加上 `-` 默认收起 `>[!danger]- 我是标注`
>[!NOTE]- 我是标注
>可选值有note abstract summary tldr info todo tip hint important
>success,check,done,question,help,faq,warning,caution,attention,failure,fail,missing
>danger,error,bug,example,quote,cite
> >[!danger] 我是标注
> >>[!bug] 我是标注
> >>>[!help] 我是标注

8. 注释（注解）：`[^注解id或注解内容或链接]` 标记为跳转注解 `[^注解id]:注解内容` 或链接
	Java [^1]

[^1]:java是一种编程语言

9. 转移符： `\`  如输出\*
# 快捷键
## 查询指令
介绍：不记得指令没关系，可以用它来查询比如：加粗，分级等指令直接使用
使用：ctrl+P

## 搜索
使用 Ctrl+O



# 插件

1. ==主题== ：AnuPpuccin
2. ==Style setting==: 样式设置 
	css样式：（在设置Style setting中进行import）
```css fold:CSS代码
{
  "anuppuccin-theme-settings-extended@@anp-theme-ext-light": true,
  "anuppuccin-theme-settings-extended@@anp-theme-ext-dark": true,
  "anuppuccin-theme-settings-extended@@catppuccin-theme-extended": "ctp-atom-light",
  "anuppuccin-theme-settings-extended@@catppuccin-theme-dark-extended": "ctp-atom-dark",
  "anuppuccin-theme-settings@@anuppuccin-theme-light": "ctp-latte",
  "anuppuccin-theme-settings@@anuppuccin-theme-dark": "ctp-mocha",
  "anuppuccin-theme-settings@@anuppuccin-accent-toggle": true,
  "anuppuccin-theme-settings@@anuppuccin-theme-accents": "ctp-accent-rosewater",
  "anuppuccin-theme-settings@@anp-colorful-frame-opacity": 1,
  "anuppuccin-theme-settings@@anp-colorful-frame-color@@dark": "#43BFBA",
  "anuppuccin-theme-settings@@anp-colorful-frame-color@@light": "#74B7C4",
  "anuppuccin-theme-settings@@anp-callout-select": "anp-callout-default",
  "anuppuccin-theme-settings@@anp-callout-color-toggle": true,
  "anuppuccin-theme-settings@@anp-callout-fold-position": true,
  "anuppuccin-theme-settings@@anp-active-line": "anp-no-highlight",
  "anuppuccin-theme-settings@@anp-toggle-preview": true,
  "anuppuccin-theme-settings@@anp-toggle-scrollbars": true,
  "anuppuccin-theme-settings@@anp-header-margin-toggle": true,
  "anuppuccin-theme-settings@@anp-header-margin-value": 20,
  "anuppuccin-theme-settings@@h1-size": 1.6,
  "anuppuccin-theme-settings@@h2-size": 1.4,
  "anuppuccin-theme-settings@@h3-size": 1.3,
  "anuppuccin-theme-settings@@h4-size": 1.2,
  "anuppuccin-theme-settings@@h5-size": 1.1,
  "anuppuccin-theme-settings@@h6-size": 1.05,
  "anuppuccin-theme-settings@@anp-layout-select": "anp-card-layout",
  "anuppuccin-theme-settings@@anp-card-shadows": true,
  "anuppuccin-theme-settings@@anp-card-layout-filebrowser": true,
  "anuppuccin-theme-settings@@anp-list-toggle": true,
  "anuppuccin-theme-settings@@anp-button-metadata-toggle": true,
  "anuppuccin-theme-settings@@anp-custom-vault-toggle": true,
  "anuppuccin-theme-settings@@anp-color-transition-toggle": true,
  "anuppuccin-theme-settings@@anp-alt-rainbow-style": "anp-simple-rainbow-color-toggle",
  "anuppuccin-theme-settings@@anp-rainbow-file-toggle": true,
  "anuppuccin-theme-settings@@anp-rainbow-folder-bg-opacity": 0.7,
  "anuppuccin-theme-settings@@anp-simple-rainbow-title-toggle": true,
  "anuppuccin-theme-settings@@anp-simple-rainbow-indentation-toggle": true,
  "anuppuccin-theme-settings@@anp-table-toggle": true,
  "anuppuccin-theme-settings@@anp-table-width": true,
  "anuppuccin-theme-settings@@anp-td-highlight": "anp-td-none",
  "anuppuccin-theme-settings@@anp-table-align-th": "center",
  "anuppuccin-theme-settings@@anp-table-width-pct": 100,
  "anuppuccin-theme-settings@@anp-alt-tab-style": "anp-alternate-tab-toggle",
  "anuppuccin-theme-settings@@anp-decoration-toggle": true,
  "anuppuccin-theme-settings@@anp-bold-custom": "anp-bold-maroon",
  "anuppuccin-theme-settings@@anp-codeblock-numbers": true,
  "anuppuccin-theme-settings@@anp-header-color-toggle": true
}
```
3. ==Code Style== : 根好代码块
	- `fold` 折叠
	- `title=""` `title:""` `fold:` `fold:""` `fold=""`设置名字
4. ==Various Complements==: 自动补全,英语补全
5. ==Advanced URI:== 链接加强
	- 使用方法obsidian://advanced-uri? 开头
	- 参数`vault=` obsidian仓库名，`filepath=` 仓库下的路径名
6. Hover Editor: 双链预览功能
7. ==templater==：模板
8. kanban: 看板
9. Thino: 可以用于随手记录
10. File Cleaner :清理没有引用的资源(如:图片)
11. Excalidraw: 流程图
12. [[git]] : [[git]]推送
13. Dataview:  内部数据库查询
14. Calendar: 日記周记