# bridza-content-pipeline

BRIDZA 内容质量管线：用 OpenCode GitHub 集成做自动化 HTML 审查，把 rf 站踩过的围栏坑（裸 JS / 双重 `</script>` / JSON-LD 失配 / hreflang 断链）堵在合并之前。

## 结构

```
.github/workflows/
  opencode-review.yml      # PR 触发：按审查清单逐项检查，阻塞级直接打回
  opencode-weekly-audit.yml# 每周一巡检：全仓扫描 + sitemap 一致性，产出周报 Issue
  anatomy-build.yml        # 手动触发：Anatomy 交互机械图解构建（qwen-plus，产物回推 anatomy-builds/）
samples/
  normal.html              # 正常样本
  broken.html              # 故意埋了 4 类问题的演示样本（JSON-LD 失配/裸 JS/双重</script>/hreflang 断）
```

## 上线前需配置

Settings → Secrets and variables → Actions：
- `DASHSCOPE_API_KEY`（已配置，model: qwen/qwen-plus，主力方案）

## 触发方式

| 方式 | 操作 |
|---|---|
| PR 审查 | 提 PR 自动触发 |
| 行级追问 | PR Files 页对具体行评论 `/oc 修复这里` |
| 修 Issue | Issue 评论 `/oc fix this` → 自动开分支提 PR |
| 手动巡检 | Actions → opencode-weekly-audit → Run workflow |
| 图解构建 | Actions → anatomy-build → Run workflow（填 slug / concept / brief） |
