---
name: review
description: 分析代码差异、可维护性和安全性，生成完整 review 报告，确保工程质量
stage: review
inputs:
  - git diff 或代码文件
outputs:
  - review_report
stop_conditions:
  - 输入缺失
  - 风险无法评估
---

# Review Skill

## 作用
统一分析代码改动，生成结构化 review 报告。  
检查维度包括：
- 代码差异（diff）
- 可维护性
- 安全性
- 风格一致性
- 测试覆盖和可靠性

## 步骤与 Checkpoints

### 1️⃣ 解析差异
- Checkpoint 1: diff 是否为空 → 若为空停止并报告
- Checkpoint 2: 是否包含新增文件或删除文件 → 标注类型
- Checkpoint 3: 检查大型重构或移动文件 → 标记潜在风险
- 输出：modified_files、changes_summary

### 2️⃣ 可维护性检查
- Checkpoint 1: 函数/方法长度是否超阈值
- Checkpoint 2: 模块/类依赖是否复杂
- Checkpoint 3: 命名是否清晰、风格一致
- Checkpoint 4: 是否存在重复代码
- 输出：maintain_issues，每条包含问题位置、类型、改进建议

### 3️⃣ 安全性检查
- Checkpoint 1: 是否有潜在 SQL/命令注入
- Checkpoint 2: 是否暴露敏感信息或凭证
- Checkpoint 3: 权限边界或访问控制检查
- Checkpoint 4: 关键逻辑异常处理是否完善
- 输出：security_issues，每条包含问题位置、类型、修复建议

### 4️⃣ 风格一致性检查
- Checkpoint 1: 是否符合团队编码规范（agent.md）
- Checkpoint 2: 注释和文档是否齐全
- Checkpoint 3: 是否符合函数短小/表达式导向原则
- 输出：style_issues，每条包含问题位置、类型、改进建议

### 5️⃣ 测试覆盖检查
- Checkpoint 1: 新增/修改代码是否有对应测试
- Checkpoint 2: 测试用例覆盖是否达到阈值
- 输出：test_issues，每条包含问题位置、类型、改进建议

### 6️⃣ 汇总报告
- 汇总所有 checkpoint 输出，生成 review_report
- review_report 格式：
  - file: 文件名
  - issues: 列表，每条包含
    - category: diff / maintain / security / style / test
    - description: 问题描述
    - recommendation: 改进措施
  - summary: 风险等级汇总（高/中/低）

---

## 输出规范
- review_report: 列表，每项包含
  - file
  - issues
  - summary

## 使用说明
- 将 git diff 或代码文件作为输入
- 可直接调用 scripts/ 中辅助检查脚本（lint、测试覆盖统计等）
- 参考文档放在 references/（编码规范、安全策略）
- 模板或示例数据放在 assets/（测试文件、样例 diff）
