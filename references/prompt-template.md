# 生图 Prompt 模板

不要直接发送带占位符的模板。先完成内容地图和文字计划，再读取 `ip-dna.md` 与 `style-dna.md`，把相关约束写入一份完整 prompt。

```text
Generate one standalone article illustration that explains a specific claim from the source text.

Source anchor:
{原句锚点或准确段落判断}

Reader takeaway:
{读者看完图应记住的具体判断，不只是主题名}

Relationship and composition pattern:
{因果/对比/转化/顺序/分层/反馈/瓶颈/状态变化 + 结构类型}

Content-to-visual mapping:
{原文概念 A → 画面对象 A；概念 B → 对象 B；关系/动作 C → 角色动作 C；结果 D → 结果对象 D}

Visual metaphor and spatial composition:
{主物件、空间关系、阅读方向、留白和视觉焦点；说明为什么这个隐喻表达本段而不是泛化主题}

Recurring character identity:
{从 ip-dna.md 提取当前视角和动作所需的外形、比例、脸部、服装、色块、材质和 signature features}

Character action:
{角色如何亲自触发关键变化；说明手脚、姿态、接触对象和动作结果}

Pose and limb plan:
- Character instances: exactly 1
- Body orientation: {正面/侧面/3/4，站/坐}
- Left arm and hand: {从左肩到左手的连续路径、唯一动作与接触对象，或 fully occluded}
- Right arm and hand: {从右肩到右手的连续路径、唯一动作与接触对象，或 fully occluded}
- Visible hands: {0/1/2，不得超过 2}
- Occlusion: {被桌面、身体或物体遮住的肢体；遮挡后不得在别处再出现}
- Legs and feet: {数量、姿态和遮挡}
- Primary action: {一个主要动作；若原概念超过两只手的动作容量，先删减或拆图}

Necessary objects only:
{3-6 个来自原文映射或核心隐喻的对象}

Chinese text plan — verbatim:
- "{短词1}" — attached to {对象/关系}, placed {位置}, styled {颜色/字形}
- "{短词2}" — attached to {对象/关系}, placed {位置}, styled {颜色/字形}
{通常 2-6 条，每项 2-8 个汉字；默认不是一个巨大标题}

Global visual style:
{从 style-dna.md 提取画幅、背景、线条、渲染、色板、空间、密度、文字、纹理、光线和情绪}

Must preserve:
{复制 ip-dna.md 中全部身份硬约束，并加入相关 style must}

Avoid:
{复制两份 DNA 中相关禁忌；加入 no generic theme illustration, no poster-sized headline, no extra text, no pseudo-text, no decorative mascot, no dense slide-like infographic, no unrelated objects, extra arms, extra hands, detached hand, floating arm, duplicated limb, fused arms, hand emerging from torso/table/object, multiple overlapping poses, ghost limbs, malformed anatomy}

Quality constraints:
One image communicates one source-backed claim. At least two visible objects and one action must map directly to the source content. The recurring character performs the indispensable conceptual action. Exactly one character instance. Exactly two arms attached naturally to the two shoulders, at most two visible hands, anatomically coherent pose, continuous shoulder-to-elbow-to-wrist-to-hand connections. Render only the planned left-hand and right-hand actions. A hidden hand is fully occluded and must not reappear elsewhere. Render only the quoted Chinese text exactly once and add no other letters, words, captions, or pseudo-text. Attach each label to its specified object or relationship. Keep the illustration readable at article-embed size. Preserve character identity and global style. Invent a fresh visual metaphor for this exact passage.
```

## 文字失败时

```text
Edit only the incorrect Chinese text area. Replace "{错误文字}" with exactly "{正确文字}". Preserve the character, action, composition, objects, colors, texture, aspect ratio and every other accepted region. Add no other text.
```

如果多次生成仍失败，减少或缩短文字，但保留最关键的对象标签、动作词和结果词。
