# 第三方来源与许可

本页汇总当前仓库复用代码、游戏素材、数据及字段核对来源。固定版本来自既有来源记录，本次文档整理没有重新抓取来源或进行法律核验。游戏素材和游戏派生内容不能套用代码许可；本项目新增代码的授权范围见源码仓库 LICENSE.md。

## stardew-save-editor 代码

上游为 [colecrouter/stardew-save-editor](https://github.com/colecrouter/stardew-save-editor)，固定提交 `2432d4ec1c4defb90a7b470f547826d2274b02f9`，原仓库 Contributors，Copyright 2024。原许可及游戏素材排除声明保留于 [licenses/stardew-save-editor.md](licenses/stardew-save-editor.md)。

| 当前代码 | 上游来源及处理 |
| --- | --- |
| src/core/upstream-xml.ts、array-tags.ts | lib/workers/xml.ts、jank.ts；去除 Comlink 暴露，作为测试参考解析器；生产写回使用保序树 |
| src/core/upstream/types | codegen/items.ts、save.ts 的类型定义 |
| src/core/upstream/ItemData.ts、ItemFactory.ts | lib/ItemData.ts 与 proxies/Item.svelte.ts 的类别工厂；保留实际使用的常量，移除 Svelte 代理，随机种子改为入参 |
| src/core/upstream/Sprite.ts、Color.ts、CharacterColors.ts | 图集裁切、染色和人物分层；颜色使用普通字段与无符号 PackedValue |
| src/core/upstream/NPCs.ts、recipe-mapping.ts、colors.ts | 原 NPC 列表、(list)/mapping.ts、codegen/colors.ts |
| src/core/upstream/bundleSerialization.ts、rooms.ts | 原社区包字符串解析与房间枚举 |
| src/core/upstream/QiEntry.ts | QiQuests.svelte.ts 的模板构造、期限计算，随机种子固定 |
| src/core/character、friendship、containers、world、players、bundles、quests | 依据 Farmer/Skills/Profession/Friendship/Recipes/Chest/GameLocation/Building/FarmAnimal/SaveFile/CommunityBundles/QiQuests 字段，改为有序树事务 |
| src/styles/base.scss 与 Vue scoped SCSS | 原 UIContainer、UIContainerSmall、UIInput、UICheckbox、UIButton、SkillBar、Professions、Wallet、EmojiRange、ItemSlot、ItemView、CharacterView、Appearance、Profiles、List、QuestList、Buildings、Bundle、JojaBundles 的主题与组件样式 |

未迁移上游的 Sentry、持久化存档备份或整套 Svelte 依赖。本地 references 研究目录不参与产品构建。

## 游戏素材与基础数据

Stardew Valley 素材、名称和游戏派生内容仍归各自权利人（包括 ConcernedApe）所有。上游声明其素材按 fair use 使用，该声明不构成 MIT 授权。本项目用于私人非商用自用，没有将游戏内容统一授予代码许可。

- `public/assets/**` 原有图片来自上游 `static/assets/**`，包括物品、服装、工具、武器、家具、职业、肖像、建筑、背景和 JunimoNote。
- `public/img/**` 来自上游 `static/img/**`，包括 favicon、wallpaper 和男女农夫身体、手臂、鞋、眼睛等分层 PNG。
- `src/data/upstream-items.json` 来自 generated/iteminfo.json；dimensions、buildings、farmanimals、cookingrecipes、craftingrecipes、qiquests 来自对应 generated 数据。
- catalog 和 runtime-items 为本地派生数据；前者用于展示/搜索，后者去除未使用文案并保留工厂及精灵字段。来源地址和固定版本继续记录，不再保存文件 SHA-256 摘要。
- GameIcon 使用既有 Cursors.png 的游戏菜单图标，裁切依据为下述结构参考中的 GameMenu.draw（16×16、y=368）；其余图标复用已有图集和人物分层。

## 中文名称、配方与说明

| 数据 | 固定来源与使用范围 |
| --- | --- |
| item-names.zh-CN.json | [MateusAquino/stardewids](https://github.com/MateusAquino/stardewids/tree/b96195eeea882e4cd415471a143b7307dc8e3aba/dist)，提交 b96195eeea882e4cd415471a143b7307dc8e3aba；来源声明游戏 1.6.15。只提取本项目既有 ID 的简体中文名称，不复制 JavaScript、图片或新增定义 |
| recipe-outputs.json、bundle-keys.json、item-exclusions.json | [juliaramosguedes/stardew-data](https://github.com/juliaramosguedes/stardew-data/tree/4e0d98119afefd766f15ee77a529db4eb71fa240/data/en-US)，提交 4e0d98119afefd766f15ee77a529db4eb71fa240；来源声明游戏 1.6.15。仅取内部键、产物 ID、标准名称与场景分类，不复制解析器或图片 |
| item-descriptions.zh-CN.json | [kronosta/stardew-data](https://github.com/kronosta/stardew-data/tree/de69cb5ce6f3708a63d53ed414b757b39b3f105e)，提交 de69cb5ce6f3708a63d53ed414b757b39b3f105e；按既有 token 或鞋靴/帽子 ID 提取中文游戏文本，不复制整个文本库，不改变物品定义。来源未核实补丁版本 |

名称源为第三方导出的游戏本地化，不能称为官方发布的数据仓库。13 项人工补译/占位标签单列 overrides；加工品按父物品组合中文名，原游戏专名按原文保留。

配方产物以限定类型和上游模板校验，不采用可能混淆数字 ID 的 outputItemName。231 个配方主要使用产物的中文名，两项金属转化另作人工名称；建筑、动物、地点、社区包和 Qi 文案为显示翻译或意译，不声称全部是官方中文原文。六项含动态参数的物品说明标为“功能概述”，不填写推测数值。以上游戏派生内容不适用代码 MIT 许可。

## 农场布局资料

- 布局定义来自 [kronosta/stardew-data 固定提交](https://github.com/kronosta/stardew-data/tree/de69cb5ce6f3708a63d53ed414b757b39b3f105e) 的 Data/Buildings、Crops、WildTrees、FruitTrees、FloorsAndPaths 和 Fences，沿用游戏原权利归属。
- 区域资料及地图/场景切片来自 [hpeinar/stardewplanner](https://github.com/hpeinar/stardewplanner/tree/f6c8dd5fba513d78b95d491a8aa77d6532c55ee6)，固定提交 f6c8dd5fba513d78b95d491a8aa77d6532c55ee6。本项目将坐标列表转换为逐行位图并建立中文地图索引，未使用非开源 V3 代码。
- Planner 代码和区域资料保留 [Apache-2.0 许可原文](licenses/stardew-planner.md)；地图和游戏切片仍属原权利人，不能套用该代码许可。来源、固定提交及图片尺寸记在 src/data/layout-sources.json。
- 神秘树阶段和树桩参考图片来自[官方维基神秘树页面](https://stardewvalleywiki.com/Mystic_Tree)，此前经 imageinfo API 核对 URL 与尺寸，保存原字节，不复制维基说明正文。
- 场景名称和用途参考中文维基的[花盆](https://zh.stardewvalleywiki.com/花盆)、[春季种子](https://zh.stardewvalleywiki.com/春季种子)、[大门](https://zh.stardewvalleywiki.com/大门)、[草](https://zh.stardewvalleywiki.com/草)、[免费仙人掌](https://zh.stardewvalleywiki.com/沙漠节#免费仙人掌)；存档规则仍以结构核对资料为准。

## 姜岛人物与主题

Birdie.png、ProfessorSnail.png、MrQi.png、IslandTrader.png、Fizz.png 来自[官方维基](https://stardewvalleywiki.com/Ginger_Island)所载游戏图片，此前经 imageinfo API 核对地址和尺寸，原字节保存在 public/assets/portraits。雷欧继续使用固定上游素材。

人物范围参考[中文姜岛列表](https://zh.stardewvalleywiki.com/姜岛)和[村民列表](https://stardewvalleywiki.com/Villagers)。src/data/island-content.json 保存每图来源、PNG 尺寸及 115 项主题物品分组来源，包含姜岛商人、核桃房、火山地牢、岛屿办事处和裁缝等页面。主题为人工整理索引，说明为简短整理，未复制整页对话或翻译库。

图片和游戏派生内容归原权利人，不适用代码 MIT；日常页面只读取本地数据，没有 Wiki 请求。

## 游戏字段核对资料

固定结构参考为 [Dannode36/StardewValleyDecompiled](https://github.com/Dannode36/StardewValleyDecompiled/tree/5225ef409e42a6159a82cf81200bf6eb315c9961)，提交 5225ef409e42a6159a82cf81200bf6eb315c9961，仅用于核对 XML 字段和初始化规则，不将游戏程序集或完整反编译源分发到产品。

核对范围包括 ToolDataDefinition、Tool、GenericTool、FishingRod、WateringCan、Pan、WeaponDataDefinition、MeleeWeapon、Slingshot；BaseEnchantment、各普通/锻造/次级附魔、Tool.AddEnchantment、Farmer.ReequipEnchantments；Building 及特殊建筑、Furniture、RandomizedPlantFurniture、IndoorPot、Object、Chest、Torch、WoodChipper、Crop、HoeDirt、Tree、FruitTree、Bush、Grass、Flooring、Fence、ResourceClump、GameLocation、FarmAnimal、AnimalHouse、NetField。

四类垃圾桶工具依据 GenericTool 的 Tool.XmlInclude 和 CreateToolInstance 支持适配；灯笼尚未宣称兼容。附魔中文名称及简短效果说明为本项目整理。

## npm 依赖

安装版本以 package-lock.json 为准，直接依赖的版本及许可字段保存在 [licenses/dependencies.json](licenses/dependencies.json)，许可原文位于 [licenses/npm](licenses/npm/)。未整体继承上游的其他依赖。旧安装日志不代表当前漏洞审计结果。
