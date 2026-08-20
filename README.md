# re7-illustrations

Re7 个人 IP 的独立文章配图 Skill。固定角色与暖纸绘本画风，从原文做认知锚点、中文短批注和配图 QA。

## 安装（当前项目）

```bash
git clone git@github.com:Return7-T/re7-illustrations.git .agents/skills/re7-illustrations
```

Grok 会扫描 `.agents/skills/`。安装后重新打开该项目会话。

## 调用

```text
Use $re7-illustrations 为下面这篇文章生成 5 张配图：

<粘贴文章>
```

只要规划：

```text
Use $re7-illustrations 先不要生图，给这篇文章做 5 张左右的 shot list。
```

## 维护

| 改什么 | 文件 |
|--------|------|
| 角色身份 | `references/ip-dna.md`、`assets/ip-reference/` |
| 画风 | `references/style-dna.md` |
| 和正文贴合 | `references/content-mapping.md` |
| 中文批注 | `references/annotation-system.md` |
| 构图 | `references/composition-patterns.md` |

本仓库为私人仓库，仅包含本 Skill，不依赖 ip-illustration-skill-builder。
