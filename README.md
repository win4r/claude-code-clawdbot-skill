# [🚀观看我的哔哩哔哩视频](https://space.bilibili.com/3493277319825652)

# claude-code-clawdbot-skill

A **Clawdbot skill** to run **Claude Code** (Anthropic) on the host via the `claude` CLI (Agent SDK).

This repo provides:
- `SKILL.md`: how Clawdbot should use this skill
- `scripts/claude_code_run.py`: a small wrapper that runs `claude -p ...` through a pseudo-terminal to avoid non-TTY hangs

## Why a wrapper?

Claude Code can behave differently when there is no TTY. In automation (e.g., cron / headless runners), `claude -p` may hang.
This wrapper uses `script -q -c ... /dev/null` to allocate a pseudo-terminal.

## Requirements

- Claude Code installed on the same host
- `claude` binary available (default expected: `/home/ubuntu/.local/bin/claude`)

Check:
```bash
claude --version
```

## Usage

Basic headless prompt:
```bash
./scripts/claude_code_run.py -p "Return only the single word OK." --permission-mode plan
```

Allow tools (least privilege recommended):
```bash
./scripts/claude_code_run.py \
  -p "Run tests and fix failures" \
  --allowedTools "Bash,Read,Edit"
```

Structured output:
```bash
./scripts/claude_code_run.py -p "Summarize this repo" --output-format json
```

---

# 中文说明

这是一个让 **Clawdbot** 在服务器上通过 **Claude Code CLI（claude）** 运行任务的 skill。

仓库包含：
- `SKILL.md`：给 Clawdbot 用的 skill 说明
- `scripts/claude_code_run.py`：对 `claude -p` 的封装（分配伪终端），用于避免在无 TTY 环境下卡住

## 使用方法

基础测试：
```bash
./scripts/claude_code_run.py -p "Return only the single word OK." --permission-mode plan
```

允许工具（建议最小权限）：
```bash
./scripts/claude_code_run.py \
  -p "运行测试并修复失败" \
  --allowedTools "Bash,Read,Edit"
```

结构化输出：
```bash
./scripts/claude_code_run.py -p "总结这个仓库" --output-format json
```
