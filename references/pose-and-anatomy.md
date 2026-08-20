# 姿态与肢体完整性

肢体正确是交付硬门槛，不是风格偏好。先把动作改写成身体真正能完成的姿态，再生成图片。

## 参考图使用规则

- `assets/ip-reference.*` 或 `assets/ip-reference/` 应优先存放单姿态参考：一张图只出现一个完整角色实例。
- `assets/character-sheet.*` 可以包含多视角、多动作，但只用于分析身份与选择姿态，不直接作为场景生图参考。
- 如果现有 `ip-reference.*` 实际是多姿态设定图，也要把它视为 character sheet。先裁出最接近当前动作的一张完整单姿态图，再只附加该裁图。
- 不要把含多个角色实例、多个姿势或分解手部的整张设定图直接传给场景生图；这会提高重复角色、鬼影肢体和多手概率。
- 裁图必须保留头、双肩、躯干和足够多的四肢连接，不能只截孤立手部。

## 动作容量

- 默认一张连续场景只出现一个角色实例；只有用户明确要求分镜或多人时才增加。
- 一个角色只承担一个主要动作。允许一个自然的辅助动作，但必须明确分配给另一只手。
- 一个角色最多只有两只手可执行动作。需要三个以上独立动作时，必须删减、拆成多图/多格，或让设备输出、空间状态与道具结果表达其余步骤。
- 不要让同一个角色同时投递资料、比较选项、搭建物体。可改为：角色只投递资料，机器输出整理结果；“判断”和“创造”作为下一张图，或作为角色面前已出现的结果对象。

## 生图前的强制姿态计划

每张图在完整 prompt 前先写并检查：

```text
Character instances: exactly 1
Body orientation: {正面/侧面/3/4，站/坐，身体与桌面或物体的关系}
Left arm: {从左肩到左肘、左腕的连续路径}
Left hand: {唯一动作与接触对象；或 fully occluded}
Right arm: {从右肩到右肘、右腕的连续路径}
Right hand: {唯一动作与接触对象；或 fully occluded}
Visible hands: {0/1/2，不得超过 2}
Occlusion: {被桌面、身体或物体遮住的肢体；遮住就不再另画一只手}
Legs and feet: {可见数量、站姿与遮挡关系}
Primary action: {一个主要动作}
Forbidden anatomy: extra arms, extra hands, detached hand, floating arm, duplicated limb, fused limbs, hand emerging from torso/table/object, overlapping poses, ghost limbs
```

若无法用这张计划解释画面，说明动作不可行，必须先简化 shot。

## Prompt 硬约束

在每份生图 prompt 中明确加入：

```text
Exactly one character instance. Exactly two arms attached naturally to the two shoulders, at most two visible hands, anatomically coherent pose, continuous shoulder-to-elbow-to-wrist-to-hand connections. Render only the planned left-hand and right-hand actions. A hidden hand is fully occluded and must not reappear elsewhere.
```

并明确排除：

```text
extra arms, extra hands, detached hand, floating arm, duplicated limb, fused arms, hand emerging from torso, hand emerging from table or object, multiple overlapping poses, ghost limbs, malformed anatomy
```

## 生图后的硬性验收

1. 数清角色实例、肩膀、手臂、手和腿。
2. 从每只可见手沿手腕、前臂、肘、上臂追溯到正确肩膀。
3. 检查桌沿、物体后方和躯干边缘，确认没有额外手、断臂或鬼影肢体。
4. 检查两只手是否与姿态计划一致；被声明遮挡的手不得在别处重新出现。
5. 任一项失败都不得交付，也不得在 QA 报告中写“通过”。

## 返工顺序

1. 优先整张重生成，删除辅助动作，只保留一个主要动作。
2. 只附加一张单姿态角色参考；减少手边道具和相互遮挡。
3. 改用清楚的侧面或 3/4 姿态，让双肩和两条手臂路径可见。
4. 若概念确实需要多个动作，拆成两张图或 2-3 格 mini comic，每格一个动作。
5. 只有在额外肢体完全孤立且删除不会损坏正确肢体时，才可局部编辑移除；否则整张重生成。
