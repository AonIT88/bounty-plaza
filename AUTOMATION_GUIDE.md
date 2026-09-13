# PR 自动化处理指南

## 概述

本指南说明如何使用自动化脚本处理 Bounty Plaza 仓库中的大量 PR。

### 功能

✅ **自动检测和关闭重复 PR**
- 基于标题和描述的关键字匹配
- 支持自定义重复规则
- 保留"正版" PR，关闭其他重复项

✅ **自动标记 PR**
- 按优先级标记 (critical/high/medium/low)
- 按类型标记 (bugfix/feature/docs/refactor)
- 按领域标记 (bedrock/smart-contract/performance/security)
- 按赏金金额标记

✅ **生成优先级列表**
- 按优先级、赏金、创建时间排序
- 导出为 JSON 报告
- 用于后续人工审核

---

## 使用方法

### 本地执行 (推荐)

#### 前置要求

```bash
# 1. 克隆仓库
git clone https://github.com/zhangjiayang6835-cyber/bounty-plaza.git
cd bounty-plaza

# 2. 安装依赖
pip install -r scripts/requirements.txt

# 3. 生成 GitHub Token
# 访问: https://github.com/settings/tokens/new
# 权限: repo, read:org
```

#### 执行脚本

```bash
# 模拟执行 (推荐先用这个测试)
export GITHUB_TOKEN=ghp_your_token_here
export DRY_RUN=true
python scripts/pr_automation.py

# 实际执行 (谨慎!)
export GITHUB_TOKEN=ghp_your_token_here
export DRY_RUN=false
python scripts/pr_automation.py
```

---

## 脚本工作流程

```
开始 → 连接仓库 → 初始化标签 → 检测重复PR → 自动标记 → 生成报告 → 结束
```

---

## 预期效果

```
🚀 Bounty Plaza PR 自动化处理系统
============================================================
✅ 已连接到仓库: zhangjiayang6835-cyber/bounty-plaza

1️⃣  初始化标签系统...
2️⃣  检测重复PR...
   已处理: 87 个重复PR
3️⃣  自动标记PR...
   已处理: 463 / 463 PR
4️⃣  生成优先级处理列表...

✅ 处理完成!
   • 已关闭重复PR: 87
   • 已标记PR: 463
   • 优先级报告: pr_report.json
============================================================
```

---

## 常见问题

**Q: 脚本会删除 PR 吗?**  
A: 不会。只是关闭 PR，历史记录全部保留。

**Q: 如何恢复关闭的 PR?**  
A: 打开 PR 页面点击 "Reopen" 按钮即可。

**Q: DRY-RUN 和实际执行有什么区别?**  
A: DRY-RUN 只显示操作，不修改任何 PR。建议先运行 DRY-RUN。

---

## 下一步

1. 审核生成的 `pr_report.json` 报告
2. 对优先级高的 PR 进行人工审核
3. 定期合并通过审核的 PR
4. 每周运行一次脚本维护 PR 队列
