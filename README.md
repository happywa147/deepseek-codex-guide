# Codex 调用 DeepSeek 备忘

## 先记住这句

在 Codex 里直接聊天，默认还是 Codex/GPT 在回答。

只有明确说：

```text
DS：……
```

才表示让 Codex 去调用 DeepSeek。

## 不要混淆两件事

说：

```text
按 DeepSeek 风格写……
```

只是让当前模型模仿一种写法，不等于真的换成 DeepSeek。

说：

```text
DS：……
```

才是把这句话交给 DeepSeek API。

简单记：

```text
风格不是模型。
DS 才是调用。
```

## 现在本机已经有的入口

终端里可以直接用：

```bash
ds "你的问题"
```

也可以用完整名字：

```bash
deepseek "你的问题"
```

这两个命令都会走同一个脚本：

```text
/Users/core-x/Documents/Claude Work/personal-agents/tools/deepseek_creative.py
```

目前默认设置是：

```text
模式：plain
模型：deepseek-v4-flash
```

`plain` 的意思是普通回答，不套“灵感、文风、初稿”那一类写作身份。

## API Key

DeepSeek 要能跑，需要本机有这个环境变量：

```bash
export DEEPSEEK_API_KEY="你的真实DeepSeek密钥"
```

如果没有设置，调用时会看到：

```text
缺少环境变量 DEEPSEEK_API_KEY。请先设置 DeepSeek API Key。
```

注意：真实 Key 不要写进文档、公开聊天记录或代码仓库。

## 在这个窗口里怎么说

只想让 DeepSeek 回答，就这样发：

```text
DS：用三句话解释资治通鉴为什么值得读
```

实际发生的是：

```text
你发 DS 口令
Codex 运行 ds 命令
DeepSeek 返回答案
Codex 把答案贴回来
```

## 两个模型怎么分工

DeepSeek 适合先给材料：

- 想法
- 标题
- 初稿
- 代码草稿
- 多个方案
- 长文本改写

Codex 适合把事情落地：

- 读项目文件
- 改真实代码
- 跑命令
- 看报错
- 修问题
- 做测试
- 最后验收

可以把它理解成：

```text
DeepSeek 先出东西。
Codex 负责判断、修改、跑通。
```

## 常用口令

只问 DeepSeek：

```text
DS：……
```

让 DeepSeek 先想，Codex 再筛：

```text
让 DS 先发散，你来筛选：……
```

让 DeepSeek 写第一版，Codex 再整理：

```text
让 DS 先写初稿，你来改好：……
```

让 DeepSeek 出技术方案，Codex 负责实现：

```text
让 DS 先写方案，你来实现：……
```

让两个模型配合到结果能用：

```text
让 DS 和你连续协作直到跑通：……
```

## 写作任务怎么用

适合文章、书稿、课程、公众号、脚本、对话体。

可以这样说：

```text
让 DS 先给 5 个开头方向，你来选出最适合我的一个：……
```

或者：

```text
让 DS 写初稿，你负责改成更清楚、更克制、更适合发布的版本：……
```

一个顺手的流程：

```text
DS 给方向
Codex 帮忙筛
DS 写初稿
Codex 改结构、删空话、补逻辑
最后 Codex 整理成可用稿
```

## 写程序怎么用

适合小工具、脚本、页面、功能设计、技术方案。

可以这样说：

```text
让 DS 先写方案，你来实现并测试：……
```

实际流程：

```text
DS 给思路或代码草稿
Codex 看当前项目结构
Codex 判断这方案能不能用
Codex 改文件
Codex 跑测试
有报错就继续修
需要时再问 DS 要另一个方案
```

更完整的口令：

```text
让 DS 和你连续协作直到跑通：做一个 Python 工具，把 Markdown 批量转 PDF，并保留标题层级。
```

## 大一点的项目怎么用

不要让 DeepSeek 一上来直接写完整项目。

更稳的说法是：

```text
让 DS 先给 3 套方案，你评估风险、选一套，然后实现：……
```

这样 DeepSeek 负责给选择，Codex 负责看项目、定方案、改代码、跑测试。

## 什么时候别绕 DeepSeek

这些事情让 Codex 直接做更好：

```text
项目真实报错
依赖安装问题
跨文件重构
数据库迁移
权限、安全、密钥相关
需要读取本机文件
需要运行测试
必须保证最终可用
```

原因很简单：DeepSeek 只返回文字；Codex 能看文件、改文件、跑命令。

## 成本和效率

省时间的用法：

```text
需要很多想法：先用 DS
需要直接跑通：Codex 主导
很简单的任务：Codex 直接做
```

可能更省成本的用法：

```text
低风险、长文本、草稿、发散：交给 DS
高风险、落地、测试、验收：交给 Codex
```

不要每件事都先走 DS。小事多绕一层，反而慢。

## 默认工作方式

以后可以按这个节奏来：

```text
你说目标
Codex 判断要不要用 DS
值得用，就让 DS 出草稿或方案
Codex 负责筛选、执行、修正、验证
最后交付能用的结果
```

最后再记一遍：

```text
DS 负责打开可能性。
Codex 负责收回来、做出来、跑起来。
```
