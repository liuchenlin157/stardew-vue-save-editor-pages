# 第三方来源与许可

上游：[colecrouter/stardew-save-editor](https://github.com/colecrouter/stardew-save-editor)。固定提交 `2432d4ec1c4defb90a7b470f547826d2274b02f9`，原仓库 Contributors，Copyright 2024。代码许可原文保存在 `licenses/stardew-save-editor.md`，保留其游戏素材排除声明。

## 复用代码

| 本项目 | 固定上游来源及处理 |
| --- | --- |
| core/upstream-xml.ts、array-tags.ts | lib/workers/xml.ts、jank.ts；去除 Comlink 暴露，原解析规则保留 |
| core/upstream/types | codegen/items.ts、save.ts；保留原类型 |
| core/upstream/ItemData.ts、ItemFactory.ts | lib/ItemData.ts、proxies/Item.svelte.ts 的完整 fromName 工厂；去 Svelte，种子改为入参 |
| core/upstream/Sprite.ts、Color.ts、CharacterColors.ts | 原图集裁切及染色算法，颜色用普通字段和 PackedValue getter |
| core/upstream/NPCs.ts、recipe-mapping.ts、colors.ts | 原 NPC 列表、(list)/mapping.ts、codegen/colors.ts |
| core/upstream/bundleSerialization.ts、rooms.ts | 原社区包字符串解析和房间枚举 |
| core/upstream/QiEntry.ts | QiQuests.svelte.ts 的模板构造和期限计算，随机种子固定 |
| core/character、containers、world、players、bundles、quests | 依据 Farmer/Skills/Profession/Friendship/Recipes/Chest/GameLocation/Building/FarmAnimal/SaveFile/CommunityBundles/QiQuests 原字段，改为保序树事务 |
| styles/base.scss、Vue scoped SCSS | 原 UIContainer、UIContainerSmall、UIInput、UICheckbox、UIButton、SkillBar、Professions、Wallet、EmojiRange、ItemSlot、ItemView、CharacterView、Appearance、Profiles、List、QuestList、Buildings、Bundle、JojaBundles；来源明细见 docs/style-parity.md |

新增适配代码及安全策略的许可见 LICENSE.md。没有将上游游戏内容套用代码许可。

## 游戏素材与数据

这些内容不适用上游代码 MIT 许可：

- `public/assets/**` 原有素材来自固定上游 `static/assets/**`：物品、服装、工具、武器、家具、职业、NPC 肖像、建筑、背景及 JunimoNote 等。
- `public/img/**` 来自 `static/img/**`：favicon、wallpaper 与男女农夫身体、手臂、鞋、眼睛等分层 PNG。
- `src/data/upstream-items.json` 来自 generated/iteminfo.json；dimensions、buildings、farmanimals、cookingrecipes、craftingrecipes、qiquests 来自对应 generated 数据。
- `catalog.json` 和 `runtime-items.json` 为离线派生数据。运行数据只移除未使用文案字段，保留类型构造所需游戏字段；索引记录固定 SHA 和原始数据摘要。

Stardew Valley 素材、名称及游戏派生内容仍归各自权利人（包括 ConcernedApe）所有。上游声明其素材按 fair use 使用；该声明不构成 MIT 授权。本项目按照你的明确要求使用对应原游戏素材，工程用于私人非商用自用。没有复制整份 Wiki 翻译库。`src/data/item-names.zh-CN.json` 仅提取 [MateusAquino/stardewids 固定导出](https://github.com/MateusAquino/stardewids/tree/b96195eeea882e4cd415471a143b7307dc8e3aba/dist) 中匹配本项目既有 ID 的简体中文游戏名称；该来源声明游戏数据为 1.6.15。未复制其 JavaScript、图片或新增物品定义。来源 SHA 和各 JSON 的 SHA-256 随名称表保存；13 项人工补译/占位说明另列 overrides，加工品显示名按父物品中文组合。该名称表仍为游戏派生内容，不套用代码 MIT 许可。

工具和武器字段参照 [StardewValleyDecompiled 固定源](https://github.com/Dannode36/StardewValleyDecompiled/tree/5225ef409e42a6159a82cf81200bf6eb315c9961)：仅用于核对 ToolDataDefinition、Tool、FishingRod、WateringCan、Pan、WeaponDataDefinition、MeleeWeapon、Slingshot 的字段和初始化规则，没有把游戏程序集或完整反编译文件复制进产品。新增适配与原上游工厂的差异见 docs/item-editing.md。GenericTool 在同一核对源中具有 Tool.XmlInclude 和 CreateToolInstance 的明确支持，补齐四种垃圾桶工具；灯笼仍未宣称存档兼容。

`recipe-outputs.json`、`bundle-keys.json` 和 `item-exclusions.json` 只摘取 [juliaramosguedes/stardew-data 固定提交](https://github.com/juliaramosguedes/stardew-data/tree/4e0d98119afefd766f15ee77a529db4eb71fa240/data/en-US) 中的内部键、产物 ID、标准名称与场景分类事实，未复制其解析器或图片；来源声明游戏 1.6.15。配方中文采用既有游戏产物中文名，两项金属转化、世界名称和 Qi 文案另作人工显示翻译/意译，不改写内部游戏 token。这些游戏派生数据仍不适用代码 MIT。完整覆盖与边界见 docs/localization-audit.md。

新增姜岛人物图片 `Birdie.png`、`ProfessorSnail.png`、`MrQi.png`、`IslandTrader.png`、`Fizz.png` 来自 [官方维基](https://stardewvalleywiki.com/Ginger_Island)所载游戏图片，经 imageinfo API 核对原图片 URL/尺寸，原字节保存在本地。`src/data/island-content.json` 保存每图来源、PNG 尺寸和 SHA-256；姜岛人物事实与 115 项物品主题整理的来源也随数据保存。没有复制维基对话或整页翻译，新增简短说明为本项目整理。图片及游戏派生内容仍归 ConcernedApe 等权利人，不套用代码 MIT；未新增运行时网络请求。

工具与武器附魔适配亦核对上述固定反编译源中的 `BaseEnchantment`、普通附魔及锻造/次级附魔类、`Tool.AddEnchantment`、`Farmer.ReequipEnchantments`、`Axe`、`Pickaxe` 和 `WateringCan`。仅实现已核实的 XML 字段与效果规则，没有分发整份核对源；中文附魔显示名及简短说明为本项目整理。支持范围见 `docs/item-editing.md`。

`GameIcon.vue` 的原游戏菜单图标使用既有 `Cursors.png`，裁切位置核对同一固定源的 `GameMenu.draw`（16×16、y=368）；其他入口图标复用既有物品目录与人物分层，不新增外部图集。

## npm 依赖

安装版本以 package-lock.json 为准，直接依赖的版本与许可字段见 `licenses/dependencies.json`，许可原文保存在 `licenses/npm/`。未整体继承 Svelte、Sentry 或上游的其他依赖。

早期安装时 npm 审计报告 0 vulnerabilities，仅作为当时记录，本轮没有重新进行网络漏洞审计。

物品说明 `src/data/item-descriptions.zh-CN.json` 从 [kronosta/stardew-data 固定提交](https://github.com/kronosta/stardew-data/tree/de69cb5ce6f3708a63d53ed414b757b39b3f105e) 的中文游戏文本中，按本项目上游既有 token 或鞋靴/帽子 ID 提取。仅用于离线显示，不改变物品定义；来源未核实补丁版本，不能据此认定与用户安装版本完全一致。文件记录来源 SHA 与所用源文件 SHA-256；六项含动态参数的说明改为标明“功能概述”的中文摘要，不填写随机数值。未复制整个文本库；游戏文本仍归原权利人，不适用本项目代码 MIT 许可。可通过 `npm run data:descriptions` 重新生成。
