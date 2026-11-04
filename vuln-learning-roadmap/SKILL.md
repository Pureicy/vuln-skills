---
name: vuln-learning-roadmap
description: "漏洞学习的路线与优先级：先学普遍简单的类建立判定直觉，再按危害程度加权深挖（CISA KEV、RCE 链、认证绕过、组件 CVE 家族）。回答「该先学什么、学到什么程度、如何判断学会了」。反触发：逐类判定信号见 web-vuln-classes；完整测试流程见 web-vuln-methodology。"
whenToUse: "Use when planning a study path for web security, deciding which vulnerability classes or CVEs to prioritize, or checking whether a learner has truly understood a given vulnerability."
---

# 漏洞学习路线

目标：把「近 2 万条公开漏洞情报」变成能力，而不是堆资料。分三步，投入按危害程度倾斜。

## 第一步：建立判定直觉（普遍/简单的类）

真实 Web 里出现频率最高的类，先学它们是为了建立「什么是真命中、什么是假阳性」的直觉：

| 类 | 常见度 | 顺序 |
|---|---|---|
| IDOR / BOLA / 越权 | ★★★★★ | 1（最多最常见） |
| SQL 注入 | ★★★★★ | 2 |
| XSS | ★★★★★ | 3 |
| 文件上传 | ★★★★ | 4 |
| LFI / 路径遍历 | ★★★★ | 5 |
| 信息泄露 | ★★★★ | 6 |
| 开放重定向 | ★★★ | 7 |
| 弱口令 / 默认口令 | ★★★ | 8 |
| CSRF | ★★★ | 9 |
| 业务逻辑 | ★★★ | 10 |

> 逐类「判定信号 + 无害探针 + 假阳性」见 `web-vuln-classes`。

## 第二步：按危害程度加权深挖（高危优先，投入最多）

| 危害 | 类 |
|---|---|
| 代码执行 | RCE、反序列化、SSTI、表达式注入 |
| 命令执行 | 命令注入、RCE 链 |
| 认证绕过 / 提权 | 认证绕过、权限提升、默认密钥 |
| 数据泄露 | SQLi 读库、任意文件读、SSRF 打内网 |
| 服务中断 | DoS |

**CISA KEV（已知在野利用）是最高优先**——正在被真实攻击利用的漏洞，学了能直接对上现实。

## 第三步：RCE 链的拼法（组合升级）

单点漏洞要拼成 RCE 才有高分：

```
信息泄露 → 认证绕过 → 后台上传 → RCE
SQLi     → 文件读写 → 写 webshell / 读凭据（仅靶场）
SSRF     → 云元数据 169.254.169.254 / 内网 → RCE/接管
LFI      → 日志投毒 / /proc/self/environ → RCE
上传     → 解析（扩展名/中间件解析洞）→ RCE
```

**先记链路的「胶水」**：哪两个洞能连起来，比单记 payload 更有用。

## 重点组件 CVE 家族（命中率最高）

| 组件 | 代表 CVE | 类型 |
|---|---|---|
| Log4j2 | CVE-2021-44228 | JNDI 注入 RCE |
| Spring | CVE-2022-22965 | RCE |
| ThinkPHP | CVE-2018-1002015 等 | RCE / SQLi |
| Struts2 | CVE-2017-5638 (S2-045) | OGNL RCE |
| Shiro | CVE-2016-4437 | 反序列化 RCE |
| Fastjson | 多起 | 反序列化 RCE |
| Weblogic | 多起 | 反序列化 / RCE |

## 学到多少才够？

- **存**（知识库，用于查）：越多越好，不占脑力。
- **精读**（真正掌握成能力）：几百到一千条精选就够了，重点是「方法论 + 高频组件 CVE + KEV」。

## 学完一个 CVE 的自检

1. 一句话说清**触发条件**？（版本、接口、输入）
2. 知道**判定信号**？
3. 有**可复现链路**？（靶场能打通，或能写出精确步骤）
4. 知道**修复/缓解**？（升级 / 关功能 / WAF 规则）

四条都答上，才叫「学会了」。
