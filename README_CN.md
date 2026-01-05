# 🔍 Skill Discovery

[🇺🇸 English](README.md) | [🇨🇳 中文文档](README_CN.md)

---

**为 AI Agent 打造的能力搜索引擎。**

Agent Skills 功能很强大，但目前的获取体验非常糟糕。

### 痛点
每次当你需要一个专业工具（比如 Rust 代码检查、生物信息分析流程、或者营销脚本）时，都会遇到这些阻碍：
1.  **难找**：在 GitHub 或各种资源站翻来翻去，浪费大量时间。
2.  **难辨**：代码安不安全？能不能跑？每次都得自己去读源码审核。
3.  **难装**：大多数仓库都很大。为了一个小功能，你得克隆整个仓库，然后手动把文件夹提取出来放到指定位置。

**感觉不是 AI 在帮你工作，而是你在伺候 AI。**

### 解决方案
我们索引并审查了 **27,000+ 个有效技能**，构建了一个专为 Agent 设计的搜索引擎。

你不需要自己去搜，Agent 会根据任务需求直接询问 API，API 会返回一条**精准的安装指令**。

**核心价值：**
*   **意图驱动**：Agent 发现缺工具 -> 询问 API -> 获得最佳匹配。
*   **外科手术式安装**：利用 Git `sparse-checkout` 技术，**只下载** 任务所需的那个技能文件夹。拒绝磁盘臃肿。
*   **安全审查**：索引库经过预先扫描。安装脚本包含防覆盖保护，绝不破坏你现有的数据。

## 📦 安装 (一键指令)

赋予 Agent 自我武装的能力。在终端运行：

```bash
TARGET="$HOME/.claude/skills/skill-discovery"; if [ -d "$TARGET" ]; then echo "⚠️ 目标目录已存在。请先手动删除。"; else mkdir -p "$HOME/.claude/skills" && git clone --depth 1 --filter=blob:none --sparse https://github.com/WupDev/skills_discovery.git /tmp/skill_discovery_tmp && (cd /tmp/skill_discovery_tmp && git sparse-checkout set skill-discovery) && mv /tmp/skill_discovery_tmp/skill-discovery "$TARGET" && rm -rf /tmp/skill_discovery_tmp && echo "✅ 安装成功！请重启您的 Agent 以激活。"; fi
```


**运行完成后，请重启您的 Agent 以激活。**

## 💡 如何使用

直接给 Agent 派发一个你还没有工具的高难度任务。

> **你：** “我需要处理一组大型基因组数据，但我现在没有相关工具。”
>
> **Agent：** *检测到能力缺失 -> 触发 skill-discovery*
>
> **Agent：** “我找到了 'deeptools' 能够满足需求。正在为您安装...”
>
> **你：** *确认安装*
>
> **Agent：** “技能已安装。请重启以使用。”

## 🛡️ 信任与安全

*   **无黑盒**：这个 Skill 本质上只是一个连接器。它向 `skills.rest` 发送查询，并接收标准的 Git 安装指令。
*   **你的掌控**：Agent 在安装新技能前，始终会寻求你的确认。
*   **隐私保护**：搜索请求在发送前会经过脱敏处理，移除个人敏感信息。

## 📄 许可证

[MIT](LICENSE)
