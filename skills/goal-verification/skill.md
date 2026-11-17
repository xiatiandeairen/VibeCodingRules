---
name: goal-verification
description: 用最初目标验证结果，不被质量幻觉干扰。对照 Intent 判断做没做到，而不是好不好。用在实现完成后、交付前、或需要验收时。
stage: verification
inputs:
  - Intent（来自 intent-compression）
  - 产出结果（来自 execution-momentum）
outputs:
  - 验证结论（是/否）
stop_conditions:
  - 因「不满意」继续实现
---

# 目标对照验证（Goal Verification）

## 作用

用最初目标验证结果，**不被质量幻觉干扰**。  
对照 Intent，判断「做没做到」，而不是「好不好」。

## 可训练行为

- 用是 / 否回答验证问题
- 不解释、不补充条件

## 步骤

1. **取 Intent**：拿出 intent-compression 阶段的目标和不做清单
2. **逐条对照**：每条用「是/否」回答：做没做到？
3. **不扩圈**：不因「可以更好」增加验证项
4. **收尾**：已满足 → 接受结果，进入低成本反思；未满足 → 明确缺啥，回到执行推进补

## 验证问题模板

对每条 Intent 目标问：
- **做没做到？** 是 / 否

对「不做什么」问：
- **有没有越界？** 是 / 否

## 自评标准

| 状态 | 含义 |
|------|------|
| ❌ 因「不满意」继续实现 | 被质量幻觉诱惑 |
| ✅ 接受「已满足但不完美」 | 可进入低成本反思 |

## 使用说明

- **调用时机**：execution-momentum 产出后立即验证
- **上游**：依赖 `intent-compression` 的 Intent + `execution-momentum` 的产出
- **下游**：验证通过 → `lightweight-reflection`；未通过 → 回到 `execution-momentum`
- **原则**：只问做没做到，不问好不好
