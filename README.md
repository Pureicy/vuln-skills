# Web 漏洞挖掘方法论 · 开源 Skill 集

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
![Platform](https://img.shields.io/badge/Platform-Codex%20%7C%20Claude%20%7C%20DSH-blue)

一套面向**网络安全初学者与学生**的白帽 Web 漏洞挖掘方法论，以「Agent Skill」格式发布，可被 Codex / Claude / DSH 等支持 skill 的工具直接加载，也可当作普通文档阅读。

> 从公开漏洞情报（nuclei 模板、NVD/CVE、CISA KEV、Exploit-DB、公开 writeup）中提炼的**方法总结**，不是武器化工具，不含可对真实系统造成破坏的 payload。

## ⚠️ 授权与伦理（必读）

这套方法**只用于你已获得书面授权、或平台规则明确覆盖的目标**：

- ✅ 可做：SRC/众测平台范围内的资产、客户书面授权的渗透测试、自己搭建的靶场（Vulhub、DVWA、自建 lab）。
- ❌ 禁止：对未授权目标发起任何探测；获取/维持 shell；植入后门；拖库；破坏数据；横向移动。
- 验证影响时用**只读探针 + 最小影响证据**（如 `id`/`whoami` 单次回显），不落持久化、不留痕。

**如果你没有授权，请只在本地靶场练习。** 违法后果自负，与本项目无关。

## 三个 Skill

| Skill | 作用 | 一句话 |
|---|---|---|
| [`web-vuln-methodology`](web-vuln-methodology/SKILL.md) | **主方法论**（怎么挖） | 侦察 → 入账 → 假设 → 探针 → 证实 → 证据 → 报告 的完整流程与判定纪律 |
| [`web-vuln-classes`](web-vuln-classes/SKILL.md) | **漏洞类速查**（挖什么） | 16 类漏洞的判定信号 / 无害探针 / 假阳性 |
| [`vuln-learning-roadmap`](vuln-learning-roadmap/SKILL.md) | **学习路线**（先学啥） | 先简单后按危害加权、KEV 优先、RCE 链、组件 CVE 家族 |

三者关系：**roadmap 告诉你先学什么 → classes 给你每类的判定方法 → methodology 把整件事串成可执行流程**。

## 目录结构

```
vuln-skills/
├── README.md               # 本文件
├── LICENSE                 # CC BY 4.0
├── CONTRIBUTING.md         # 贡献指南
├── .gitignore
├── web-vuln-methodology/
│   └── SKILL.md
├── web-vuln-classes/
│   └── SKILL.md
└── vuln-learning-roadmap/
    └── SKILL.md
```

## 安装

复制到你的 skill 根目录即可（不同工具路径不同，任选其一）：

```bash
# Codex / Claude Code
cp -r web-vuln-methodology web-vuln-classes vuln-learning-roadmap ~/.codex/skills/

# DSH
cp -r web-vuln-methodology web-vuln-classes vuln-learning-roadmap ~/.agents/skills/
```

## Skill 结构约定

每个 skill 一个文件夹，核心是 `SKILL.md`（含 YAML frontmatter 的 `name` / `description` / `whenToUse`），复杂内容放 `references/`，按需加载、不占上下文。

## 贡献

欢迎提交 Issue 和 PR，规范见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 许可

[CC BY 4.0](LICENSE) —— 可自由学习、引用、修改、商用，署名即可。
