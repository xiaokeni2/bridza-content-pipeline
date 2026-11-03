# bridza-content-pipeline

BRIDZA 内容质量管线：用 OpenCode GitHub 集成做自动化 HTML 审查，把 rf 站踩过的围栏坑（裸 JS / 双重 `</script>` / JSON-LD 失配 / hreflang 断链）堵在合并之前。

## 结构

```
.github/workflows/
  opencode-review.yml      # PR 触发：按审查清单逐项检查，阻塞级直接打回
  opencode-weekly-audit.yml# 每周一巡检：全仓扫描 + sitemap 一致性，产出周报 Issue
samples/
  normal.html              # 正常样本
  broken.html              # 故意埋了 4 类问题的演示样本（JSON-LD 失配/裸 JS/双重</script>/hreflang 断）
```

## 上线前需配置

Settings → Secrets and variables → Actions 添加其一：
- `ANTHROPIC_API_KEY`（model: anthropic/claude-sonnet-5-5）
- 降本可换 `DEEPSEEK_API_KEY`（workflow 内解开注释，model 改 deepseek/deepseek-chat）

## 触发方式

| 方式 | 操作 |
|---|---|
| PR 审查 | 提 PR 自动触发 |
| 行级追问 | PR Files 页对具体行评论 `/oc 修复这里` |
| 修 Issue | Issue 评论 `/oc fix this` → 自动开分支提 PR |
| 手动巡检 | Actions → opencode-weekly-audit → Run workflow |
