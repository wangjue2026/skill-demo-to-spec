# 🔄 原型逆向与设计说明书转换技能 (Demo-to-Spec Converter) v2.0

> **定位**：将现有 HTML/Alpine/Tailwind 非标原型 Demo，基于内部 Common Design 与 IDUX 组件库规范进行**确定性 1:1 语法逆向提纯与语义映射**，输出包含界面线框图、置顶组件映射表与异常状态机的标准《体验设计方案说明书》（100% 离线 Zero CDN），并同步剥离提纯 TypeScript 类型与独立 Mock 数据包。

---

## 🌟 为什么需要本技能？

| 维度 | 直接把 HTML Demo 搬到内部平台 | 使用本技能转换后进入平台 |
| :--- | :--- | :--- |
| **底层兼容性** | ❌ Tailwind Preflight 重置样式污染全局，Alpine.js 指令与 Vue 3 冲突 | ✅ 100% 规范化 Vue 3 结构，完美接入平台统一 Layout |
| **组件质量** | ❌ 充斥手写 `<table>`、原生 `<select>`、手绘 Div 弹窗，无法复用 | ✅ 语义映射到标准 IDUX 组件（`IxTable`, `IxSelect`, `IxDrawer` 等） |
| **设计一致性** | ❌ 硬编码十六进制色值，脱离内部设计系统与主题换肤 | ✅ 严格对齐 Common Design 规范与 Token 变量 |
| **研发交付成本** | ❌ 研发面对几千行代码如同“嚼蜡重写”，极易丢掉关键交互 | ✅ 研发拿到标准线框图、组件规范、TypeScript 契约与独立 Mock 数据包，提效 70% |
| **内网离线可用** | ❌ 外网 CDN 脚本（如 jsdelivr）在内网加载超时阻塞 | ✅ 100% 离线自包含，纯内嵌 HTML/CSS 拓扑卡片流，零外部网络依赖 |

---

## 📁 目录架构说明

```text
skill-demo-to-spec/
├── SKILL.md                          # ⭐️ 技能核心规约与 Quality Gate 10 大硬核门禁
├── execution-sop.md                  # ⭐️ 标准作业程序 (SOP)：AI 稳定执行与人工核验规程
├── README.md                         # 本手册
│
├── scripts/                          # 🛠️ 确定性逆向工具链
│   └── extract_demo_dom.py           # ⭐️ DOM 物理真值基准提取器 v2.0 (栅格/资产/控件/列宽)
│
├── 01-reverse-parser/                # 逆向解析指南
│   ├── 1.0-in-memory-distillation.md # Demo 标杆案例即时认知蒸馏指南 (无需中间物落库)
│   ├── 1.1-topology-extractor.md     # 页面拓扑与路由关系提取规则 (容器三问)
│   ├── 1.2-dom-semantic-rules.md     # 非标 DOM 识别为语义组件规则 (排版保真铁律)
│   ├── 1.3-data-types-builder.md     # 数据模型反推与 TypeScript 契约生成规范
│   └── 1.4-interaction-extractor.md  # 交互逻辑与联动状态机逆向提取指南
│
├── 02-design-assets/                 # [独立资产副本] 内部设计与 IDUX 组件标准库
│   ├── idux-component-map.md         # ⭐️ IDUX 组件映射全表与使用/禁止准则 (位于 components/ 子目录)
│   ├── tokens-cheatsheet.md          # 色彩、尺寸、网格 Token 速查表
│   ├── page-templates/               # 页面类型模板标准 (表格型、看板型、主从型等)
│   └── components/                   # 各组件细化规范 (表格、抽屉、表单、标签等)
│
├── 03-spec-generator/                # 标准设计说明书生成引擎 (100% 离线纯净化)
│   ├── spec-template.md              # 逆向专属《设计方案说明书》3章标准模板 (纯内嵌拓扑)
│   ├── global-overview-template.md   # 1+N 分册专用「全局总控」模板 (纯 HTML/CSS 节点流)
│   ├── wireframe-syntax.md           # ⭐️ 界面线框图排版语法 (含 4 大特化资产线框原语)
│   └── quality-gate.md               # ⭐️ 交付质量门禁 10 大硬核铁律 (QG-00 ~ QG-09)
│
├── 04-code-packager/                 # 研发加速层代码生成指南
│   ├── mock-exporter.md              # 数据模型与 Mock 提纯规范 (types.ts + mock-data.ts)
│   ├── chart-extractor.md            # ECharts 纯净配置提取规范 (charts.config.ts)
│   └── visual-component-extractor.md # 特化可视化 SFC 组件 (拓扑链/散点时间线) 封装
│
└── examples/                         # 📚 标杆案例参考库
    ├── README.md                     # 标杆案例索引 (单模块样本 + 方案七 1+N 官方工程)
    └── sample-probe-config/          # 单模块独立转换黄金范本 (监控配置中心)
```

---

## 🛠️ 核心逆向工具：`extract_demo_dom.py` v2.0

在处理任何 HTML 原型前，**必须首先运行确定性逆向提取脚本**，获得不可篡改的《物理真值基准表》：

```bash
python3 SKillS/skill-demo-to-spec/scripts/extract_demo_dom.py [目标HTML路径] [--json]
```

### v2.0 增强能力：
1. **页面空间骨架与容器栅格嗅探**：精准识别 `30%:40%:30%` 三栏、左侧 `240px` 侧栏 + 右侧主面板、`grid-cols-N` 等分大盘及 `x-collapse` 折叠状态；
2. **四大类特化可视化资产专属嗅探**：自动标记时序指标走势图、端到端 5 节点网络诊断拓扑链、三色底带离散散点折线时间线、体验质量 SLO 分级标尺；
3. **严谨表格结构解析**：精准提取所有 `<th>` 真实文字与宽度 Token（如 `40px`、`130px`、`280px`），并识别 `[复选框]` 全选列与 `[列设置]` 图标列，**绝对不漏一列**；
4. **全类型表单与筛选控件提取**：完整覆盖 Input placeholder、Select 全部选项、Radio 单选、Checkbox 多选、Switch 开关及起止时间选择器；
5. **抽屉与模态浮层提取**：提取 `x-show` 表达式、宽度（如 `640px` / `520px`）与滑出方向。

---

## 🚦 交付质量门禁 (Quality Gate 10 铁律)

所有产物交付前必须执行 10 项内存核验，10/10 全绿方可通过：
- **QG-00 [绝对阻断] 零发挥与物理真值 100% 镜像**：无未在源 HTML 出现的卡片/数字/按钮/emoji
- **QG-01 容器结构与空间栅格保真度**：30%:40%:30%、左侧 240px 侧栏 + 右侧工作台 100% 保真
- **QG-02 表头列数与文案 100% 吻合**：包含全选复选框列与列设置列，原原型几列就几列
- **QG-03 筛选控件与占位符吻合**：占位符与下拉选项 100% 逐字对应，表单左 Label 右 Control
- **QG-04 状态徽标与枚举保真度**：状态 Tag 枚举与颜色 Token 对应，严禁自创
- **QG-05 100% 离线与内网兼容性**：100% 杜绝任何外网 CDN，使用纯 HTML/CSS 节点拓扑流
- **QG-06 组件语义化映射精准度**：手写元素严格映射为 IDUX 标准组件与 Token
- **QG-07 特化可视化资产识别保真度**：趋势图、拓扑链、散点时间线、仪表盘保真提取，严套通用组件
- **QG-08 交互行为细则与状态机完备度**：包含《交互细则大表》与 Loading/Empty/Error/防重锁四态
- **QG-09 复杂方案 1+N 分册铁律与可运行契约**：页面数 ≥2 强制拆分 00 总控 + N 个分册，契约可直接运行

---

## 🚀 快速上手与使用方式

在对话中输入以下任意自然语言指令即可触发：

```text
“转换demo：请帮我把 DEM-应用.html 转换为标准设计说明书”
“请将 Demos/07-方案七 整个方案包逆向提取出设计说明书与数据契约”
“对 DEM-用户详情.html 进行逆向分析，映射到 IDUX 组件并输出说明书”
```

### 交付成果物：
1. **《[方案名] 体验设计方案说明书》**（`.html`）：
   - 第一章：解决方案全景与页面架构拓扑（清单大表 + 纯内嵌离线拓扑节点流）
   - 第二章：核心页面与抽屉 **【置顶组件映射表】+【居中结构线框图】+【🎨样式Token字典】+【🧭交互细则大表】+【底部批注】**
   - 第三章：页面体验与异常保护规则（状态机完备性大表 + 研发接入确认）
2. **`types.ts`**：提取完备的业务实体 TypeScript 接口定义
3. **`mock-data.ts`**：完全与 DOM 解耦、可直接被 Vue 3 导入调用的静态数据集
4. **特化物料（按需）**：`visual-components/*.vue` (拓扑链/散点时间线 SFC) + `charts.config.ts` (ECharts 纯配置)
