# Wayward-CN

Wayward 游戏简体中文汉化项目。基于官方英文原文重新译制，参考 PlotNarrater/wayward-chinese-language 项目的术语体系。

---

## 当前进度

**本体：3736 / 5245 已翻译（71.2%）**

覆盖率详情：

| 状态 | 已翻译 | 剩余 | 说明 |
|------|--------|------|------|
| 神祇 / 诅咒 / 魔法属性 | 全部覆盖 | — | 参考项目未翻译，本项目已补全 |
| 属性 / 技艺 / 品质 / 状态 | 全部覆盖 | — | |
| 动作 (action) | 99/146 | 47 | 上游新增动作待翻译 |
| 物品 (item) | 738/839 | 101 | 新物品名称待翻译 |
| UI 文本 (ui) | 664/925 | 261 | |
| 游戏消息 (message) | 692/891 | 199 | |
| 键位绑定 (bindable) | 107/245 | 138 | |
| 输入/按键 (input) | 6/132 | 126 | 参考项目有意保留英文 |

**Mod：**
- starterquest — 已翻译
- tars — 已翻译
- debugtools — 已翻译
- balancingtools — 已翻译
- oddmagicks — 已翻译

---

## 目录结构

```
Wayward-CN/
├── upstream/                    # 官方英文原文（禁止修改）
│   ├── english-language/        # 游戏本体
│   │   └── english.json
│   ├── starterquest/lang/
│   │   └── english.json
│   ├── tars/lang/
│   │   └── english.json
│   ├── debugtools/lang/
│   │   └── english.json
│   ├── balancingtools/lang/
│   │   └── english.json
│   └── oddmagicks/lang/
│       └── english.json
│
├── translation/                 # 中文翻译（镜像 upstream 结构）
│   ├── english-language/
│   │   └── chinese.json
│   ├── starterquest/lang/
│   │   └── chinese.json
│   ├── tars/lang/
│   │   └── chinese.json
│   ├── debugtools/lang/
│   │   └── chinese.json
│   ├── balancingtools/lang/
│   │   └── chinese.json
│   └── oddmagicks/lang/
│       └── chinese.json
│
└── glossary.md                  # 术语表（所有翻译的唯一参考标准）
```

规则：**`upstream/` 禁止修改，翻译一律放入 `translation/`**，路径结构与 upstream 一一对应。

---

## 术语表

`glossary.md` 是翻译的**唯一真相源**。任何翻译必须遵循术语表中的译法。

术语表涵盖：
- 核心游戏概念（curse/诅咒、deity/神祇、doodad/设施 等）
- 神祇系统（evil/邪恶、chaos/混沌、good/善良 等）
- 诅咒系统（horde/亡灵、shadows/暗影移动 等）
- 诅咒/魔法属性词缀（powerAttack/凶残·虚弱 等）
- 状态 / 属性 / 技艺
- 品质等级（normal/普通、superior/良质 等）
- 物品强化系统（upgrade/升格、enhance/强化 等）
- 火系统 / 材质 / 液体 / 时间 / 动作动词
- 常用句式（Increases chance of success./提高成功率。）

如果需要新增术语，先在 `glossary.md` 中确定译法，再修改翻译文件。术语表本身就是协作工具——有异议先在表中讨论。

---

## 翻译规则

### JSON 格式

1. **不修改 key**。仅翻译 value，key 名称与 upstream 保持一致。
2. **保留上游结构**。不要增删字段、改变数组长度或嵌套层级。
3. **保留所有占位符**：`{0}`、`{1}`、`{TARGET}`、`{TOOL}`、`{DEITY}`、`{NEW_NAME}` 等。
4. **保留格式标记**：`{*+5*}`、`{.HIDDEN:0 }`、`{#--TEXT-PRIMARY:...}` 等。
5. **保留随机词组结构**：`{%a:b:c:d}` 仅替换内部文本，不破坏结构。
6. **保留魔法属性引用**：`{$MAGIC:HURLING__THROW_DAMAGE}` 不可翻译。
7. **保留神祇引用**：`{$DEITY:GOOD}` 不可翻译。
8. **保留条件占位符**：`{TARGET??fallback}`、`{TOOL? with {TOOL}}`、`{TRADE?...:...}` 等保持结构完整。

### 翻译风格

1. **简洁**。游戏内 UI 空间有限，尽量短。
2. **自然**。避免机翻腔，读起来像母语者写的。
3. **游戏化**。保持生存/Roguelike/奇幻风格。
4. **奇幻感**。神祇、诅咒、魔法相关文本应带有神秘和压迫感。
5. **术语统一**。同一个英文词在所有位置翻译为同一个中文词（参考 glossary.md）。
6. **句式一致**。重复出现的描述文字（如"提高成功率"）保持相同译法。

### 中文排版

- 中文与英文/数字之间加空格：`+5 力量`、`HP 回复`
- 描述文本使用中文全角标点（，。！？……）
- UI 按钮/标签可使用半角标点
- 省略号用 `……`（U+2026）而非 `...`

---

## 如何继续翻译

### 通用流程

1. **查术语表**。翻译前先看 `glossary.md`，确认术语译法。
2. **打开英文原文**。在 `upstream/` 中找到对应文件。
3. **打开中文文件**。在 `translation/` 中找到同名文件（文件名改为 `chinese.json`）。
4. **翻译**。找到 value 仍为英文的条目，按规则翻译。
5. **验证 JSON**。翻译后的文件必须是合法 JSON。可用 `python3 -m json.tool chinese.json > /dev/null` 检查。
6. **提交**。按模块提交，commit message 如 `translate: curse events`。

### 翻译优先级

按对游戏体验的影响排序：

1. **高优先级**：item（物品名）、ui（界面文本）、message（游戏消息）、action（动作名/描述）
2. **中优先级**：bindable（键位）、usableActionType（可用动作类型）、milestone（成就）
3. **低优先级**：input（按键名）——建议保留英文，与键盘标识对应
4. **暂缓**：customModifier、gameOptionsIcon 等新系统，需确认游戏内实际用途后再翻译

### 查找未翻译条目

未翻译的条目 value 与 upstream 中的英文原文完全相同。可以用以下方式定位：

```bash
# 对比两个文件，找出 value 相同的 key
python3 -c "
import json
en = json.load(open('upstream/english-language/english.json'))
cn = json.load(open('translation/english-language/chinese.json'))
for sec in cn['dictionaries']:
    if sec in en['dictionaries']:
        for k in cn['dictionaries'][sec]:
            if k in en['dictionaries'][sec]:
                if cn['dictionaries'][sec][k] == en['dictionaries'][sec][k]:
                    print(f'{sec}.{k}')
"
```

### AI 辅助翻译

允许使用 ChatGPT / Claude / CodeWhale / Gemini 等工具辅助翻译，要求：

1. 将 `glossary.md` 作为术语约束提供给 AI
2. 将本 README 中的翻译规则和 JSON 格式要求提供给 AI
3. 人工校对 AI 输出：检查占位符是否完整、术语是否一致、JSON 是否合法
4. 不直接提交未经检查的 AI 翻译

---

## 游戏更新后的同步流程

当上游游戏更新，`upstream/` 中的英文文件发生变化时：

1. **更新 upstream**：`git pull` 或手动更新 `upstream/` 目录。
2. **识别变更**：对比新旧 `english.json`，找出新增/修改/删除的 key。
3. **处理新增 key**：在 `chinese.json` 中添加对应条目的翻译。
4. **处理修改 key**：如果英文原文变更，检查中文翻译是否仍然匹配。
5. **处理删除 key**：从 `chinese.json` 中移除已不存在的条目（可选，残留不会导致错误但会增大文件体积）。
6. **更新术语表**：如果有新增术语，补充到 `glossary.md`。

参考项目 PlotNarrater/wayward-chinese-language 的 `CONTRIBUTING.md` 中包含自动化 diff/merge 脚本的思路，可参考实现。

---

## Git 工作流

### 提交规范

```
translate: <模块> - <描述>
```

示例：

```
translate: curse events
translate: item - weapons
translate: ui - crafting panel
translate: starterquest
```

避免无意义的提交信息如 `update`、`fix`、`translate`（无法定位内容）。

### 分支策略

- `main`：稳定翻译版本
- 功能分支：较大范围的翻译工作建议在独立分支进行，完成后合并

---

## 参考资源

- 官方英文原文：[WaywardGame/english-language](https://github.com/WaywardGame/english-language)
- 官方 Mod 英文原文：各 mod 仓库的 `lang/english.json`
- 参考中文项目：[PlotNarrater/wayward-chinese-language](https://github.com/PlotNarrater/wayward-chinese-language)
- Wayward 官方：[Wayward Game](https://www.waywardgame.com/)

---

## 贡献

欢迎 PR。提交前请确认：

- JSON 格式正确
- 占位符未损坏（`{0}`、`{TARGET}`、`{$MAGIC:...}` 等）
- 术语符合 `glossary.md`
- 翻译条目与 `upstream/` 的 key 结构一致
- 不包含无关修改
