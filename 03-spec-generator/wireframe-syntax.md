# 界面线框图排版与语法规范 (Wireframe Syntax)

> 💡 **核心定位**：
> 说明书第二章中的线框图是内部平台研发能够 1:1 像素级还原 Demo 的核心施工依据。
> 线框图必须采用结构化 HTML/CSS（`.wf-shell` 原语体系），**绝对禁止使用粗糙 ASCII 字符画**，并严格遵守物理真值第一与零脑补铁律！

---

## 一、排版核心铁律 (Wireframe Cardinal Rules)

1. **结构五步装配顺序**：
   每个页面/抽屉小节必须严格按此顺序编排：
   1. `页面定位与核心任务`（业务目标、适用角色、路由 Path、选用模板）
   2. `【置顶】组件选型与映射清单大表`（6 列表头置于线框图上方）
   3. `【居中】结构线框示意图`（结构化 HTML/CSS，真实排版与比例）
   4. `【🎨 若含特化资产】样式 Token 与工程还原字典大表`（尺寸、Hex 色值、透明度、边框圆角、状态机颜色）
   5. `【🧭 交互动线】核心交互动线与操作行为细则大表` + `【底部】设计批注 (wf-annotation)`
2. **UI 文案 100% 真实纯净（零脑补）**：
   - 线框图内的所有按钮、标题、标签、表头、占位符必须是源 HTML 中的真实业务文案；
   - 严禁在 UI 文本中写入标记代码（如严禁写 `立即排障 (EP-01)`）；
   - **⚠️ 宏观指标卡片铁律**：仅当源 Demo 中实际存在时方可绘制！文案、数值、占比必须 100% 逐字取自源 HTML，**严禁脑补虚构“较昨日+2%”或自创指标卡**！
3. **空间栅格比例物理镜像**：
   - 原原型采用 30%:40%:30% 三栏，线框图就必须展现 30%:40%:30% 三栏；
   - 原原型采用左侧 240px 侧栏 + 右侧主工作台，线框图就必须体现该两栏布局，严禁压平。
4. **表单必须遵循左右结构**：
   - 左侧为文本标题（Label，固定宽并左对齐），右侧为控件（Control），严禁上下垂直堆叠。

---

## 二、标准管理后台线框图模版 (Standard Admin Layout)

```html
<div class="wf-container">
  <div class="wf-label">📐 [页面名称] 界面结构线框示意图</div>
  <div class="wf-shell">
    <!-- 顶栏/面包屑 -->
    <div class="wf-header">
      <span>监控中心 / 访问体验监控 / <b>应用体验</b></span>
      <div><span class="tag">page-table-overview</span></div>
    </div>
    
    <div class="wf-body">
      <!-- 仅当源 Demo 真实存在卡片时才渲染卡片区，文案 100% 对应源 Demo -->
      <div class="wf-row">
        <div class="wf-card wf-col">
          <span class="wf-label">监控应用总数</span>
          <div style="font-size:18px;font-weight:700;color:var(--blue);">128</div>
        </div>
        <div class="wf-card wf-col">
          <span class="wf-label">异常应用数</span>
          <div style="font-size:18px;font-weight:700;color:var(--danger-t);">12</div>
        </div>
      </div>

      <!-- 工具栏与筛选区 (占位符与下拉值 100% 逐字对应源 HTML) -->
      <div class="wf-row" style="background:#F8FAFC;padding:8px 12px;border-radius:2px;align-items:center;">
        <span class="wf-btn-primary">+ 新增监控应用</span>
        <span style="margin-left:auto;color:var(--text-sub);font-size:12px;">筛选：</span>
        <span style="display:inline-block;width:120px;height:24px;border:1px solid #D3D7DE;background:#FFF;padding:2px 6px;font-size:11px;">所有应用协议 ▾</span>
        <span style="display:inline-block;width:160px;height:24px;border:1px solid #D3D7DE;background:#FFF;padding:2px 6px;margin-left:8px;font-size:11px;">搜索应用名称...</span>
      </div>

      <!-- 核心表格区 (表头列数与文案 100% 逐列对应源 HTML <th>) -->
      <div class="wf-table">
        <div class="wf-th">
          <span style="width:5%;">[✔]</span>
          <span style="width:25%;">应用名称</span>
          <span style="width:15%;">类型</span>
          <span style="width:15%;">平均时延</span>
          <span style="width:15%;">丢包率</span>
          <span style="width:15%;">健康状态</span>
          <span style="width:10%;text-align:right;">操作</span>
        </div>
        <div class="wf-tr">
          <span style="width:5%;">☑</span>
          <span style="width:25%;"><b>企业协同 OA 系统</b></span>
          <span style="width:15%;">SaaS</span>
          <span style="width:15%;">32ms</span>
          <span style="width:15%;">0.0%</span>
          <span style="width:15%;"><span class="tag" style="background:var(--green-b);color:var(--green-t);border-color:var(--green-bd);">正常</span></span>
          <span style="width:10%;text-align:right;"><a href="#" style="color:var(--blue);">链路排障</a></span>
        </div>
      </div>
    </div>
  </div>

  <!-- 底部设计批注 -->
  <div class="wf-annotation">
    💡 <b>架构定位</b>：采用「概览大盘 + 查询表格 + 侧拉抽屉」的标准 B 端监控大盘模式。<br/>
    🧭 <b>CRUD 闭环</b>：<b>查</b>＝顶部筛选条件过滤；<b>诊断</b>＝点击行末【链路排障】滑出右侧 640px 详情抽屉。<br/>
    🛡️ <b>状态保护</b>：表格查询期间禁用筛选项，表格居中显示 Spin 加载态。
  </div>
</div>
```

---

## 三、四大特化可视化资产线框图原语 (Specialized Visual Wireframes)

> [!CAUTION]
> **绝对禁止套用基础 UI 组件**！遇到四大特化可视化资产时，采用以下高保真结构排版：

### 1. 🌐 网络诊断链路拓扑 (`DemTopologyChain`) 线框原语
```html
<div class="wf-card" style="background:#FAFBFD;padding:16px;">
  <div class="wf-label" style="margin-bottom:12px;">🌐 端到端网络诊断链路拓扑</div>
  <div style="display:flex;align-items:center;justify-content:space-between;padding:12px 16px;background:#FFF;border:1px solid #E1E5EB;border-radius:4px;">
    <!-- 节点 1: 终端 -->
    <div style="display:flex;flex-direction:column;align-items:center;">
      <div style="width:40px;height:40px;border-radius:50%;border:2px solid #12A679;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:bold;color:#12A679;background:#FFF;">终端</div>
      <span style="font-size:11px;color:#2F3540;margin-top:4px;">ThinkPad X1</span>
    </div>
    <!-- 连线段 1 -->
    <div style="flex:1;margin:0 8px;display:flex;flex-direction:column;align-items:center;">
      <span style="font-size:9px;color:#12A679;background:#E6F8F2;border:1px solid #B7EB8F;padding:1px 4px;border-radius:2px;margin-bottom:2px;">正常</span>
      <div style="width:100%;height:2px;background:#12A679;position:relative;">
        <span style="position:absolute;right:0;top:-4px;font-size:8px;color:#12A679;">▶</span>
      </div>
    </div>
    <!-- 节点 2: POP -->
    <div style="display:flex;flex-direction:column;align-items:center;">
      <div style="width:40px;height:40px;border-radius:50%;border:2px solid #12A679;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:bold;color:#12A679;background:#FFF;">POP</div>
      <span style="font-size:11px;color:#2F3540;margin-top:4px;">深圳POP</span>
    </div>
    <!-- 连线段 2: 异常段 -->
    <div style="flex:1;margin:0 8px;display:flex;flex-direction:column;align-items:center;">
      <span style="font-size:9px;color:#F52727;background:#FFF1F0;border:1px solid #FFA39E;padding:1px 4px;border-radius:2px;margin-bottom:2px;">RTT 188ms | 丢包 4.2%</span>
      <div style="width:100%;height:2px;background:#F52727;position:relative;">
        <span style="position:absolute;right:0;top:-4px;font-size:8px;color:#F52727;">▶</span>
      </div>
    </div>
    <!-- 节点 3: 连接器 (告警) -->
    <div style="display:flex;flex-direction:column;align-items:center;">
      <div style="width:40px;height:40px;border-radius:50%;border:2px solid #F52727;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:bold;color:#F52727;background:#FFF;">连接器</div>
      <span style="font-size:11px;color:#F52727;margin-top:4px;font-weight:bold;">总部01</span>
    </div>
    <!-- 连线段 3 -->
    <div style="flex:1;margin:0 8px;display:flex;flex-direction:column;align-items:center;">
      <span style="font-size:9px;color:#12A679;background:#E6F8F2;border:1px solid #B7EB8F;padding:1px 4px;border-radius:2px;margin-bottom:2px;">正常</span>
      <div style="width:100%;height:2px;background:#12A679;position:relative;">
        <span style="position:absolute;right:0;top:-4px;font-size:8px;color:#12A679;">▶</span>
      </div>
    </div>
    <!-- 节点 4: 应用 -->
    <div style="display:flex;flex-direction:column;align-items:center;">
      <div style="width:40px;height:40px;border-radius:50%;border:2px solid #CBD5E1;display:flex;align-items:center;justify-content:center;font-size:10px;font-weight:bold;color:#475569;background:#FFF;">应用</div>
      <span style="font-size:11px;color:#2F3540;margin-top:4px;">OA系统</span>
    </div>
  </div>
</div>
```

### 2. 📊 访问体验散点折线时间线 (`DemScatterTimeline`) 线框原语
```html
<div class="wf-card" style="background:#FAFBFD;padding:16px;">
  <div class="wf-label" style="margin-bottom:8px;">📊 访问体验离散时序态势图 (三色底带 + 采样散点 + 垂直联动标尺)</div>
  <div style="height:120px;background:#FFF;border:1px solid #E1E5EB;border-radius:2px;position:relative;overflow:hidden;">
    <!-- 三色底带 -->
    <div style="height:38px;background:rgba(18,166,121,0.06);border-bottom:1px dashed #E2E8F0;display:flex;align-items:center;padding-left:8px;font-size:10px;color:#12A679;">正常区间</div>
    <div style="height:38px;background:rgba(250,114,27,0.05);border-bottom:1px dashed #E2E8F0;display:flex;align-items:center;padding-left:8px;font-size:10px;color:#FA721B;">一般区间</div>
    <div style="height:44px;background:rgba(245,39,39,0.05);display:flex;align-items:center;padding-left:8px;font-size:10px;color:#F52727;">差区间</div>
    
    <!-- 垂直蓝色交互标尺 (贯穿选中散点) -->
    <div style="position:absolute;left:55%;top:0;bottom:0;border-left:1.5px dashed #1C6EFF;display:flex;flex-direction:column;align-items:center;">
      <span style="font-size:8px;color:#1C6EFF;margin-top:-2px;">▼</span>
    </div>
    
    <!-- 采样散点 (正常绿点、选中带光环红点) -->
    <div style="position:absolute;left:20%;top:20px;width:8px;height:8px;border-radius:50%;background:#12A679;border:1.5px solid #FFF;"></div>
    <div style="position:absolute;left:35%;top:24px;width:8px;height:8px;border-radius:50%;background:#12A679;border:1.5px solid #FFF;"></div>
    <div style="position:absolute;left:55%;top:95px;width:10px;height:10px;border-radius:50%;background:#F52727;border:2px solid #FFF;box-shadow:0 0 0 3px rgba(28,110,255,0.4);"></div>
    <div style="position:absolute;left:75%;top:22px;width:8px;height:8px;border-radius:50%;background:#12A679;border:1.5px solid #FFF;"></div>
  </div>
</div>
```

### 3. 📈 时序指标走势图 (ECharts Trend Chart) 线框原语
```html
<div class="wf-card" style="padding:16px;">
  <div class="wf-label" style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px;">
    <span>📈 应用往返时延 (RTT) 与丢包率时序走势</span>
    <span style="font-size:11px;color:var(--text-sub);">近 24 小时 · 采样间隔 5min</span>
  </div>
  <div style="height:140px;background:#FAFBFD;border:1px dashed #CBD5E1;border-radius:2px;display:flex;align-items:center;justify-content:center;position:relative;">
    <!-- 告警红虚线基线 -->
    <div style="position:absolute;left:30px;right:20px;top:40px;border-top:1px dashed #D9363E;display:flex;justify-content:flex-end;">
      <span style="font-size:9px;color:#D9363E;background:#FFF;padding:0 4px;margin-top:-8px;">告警阈值基线 100ms</span>
    </div>
    <span style="color:#6F7785;font-size:11px;">[ECharts 渲染区: charts.config.ts -> getAppLatencyChartOption]</span>
  </div>
</div>
```

### 4. ⏱️ 体验质量 SLO 分级标尺线框原语
```html
<div class="wf-card" style="padding:14px;">
  <div class="wf-label">⏱️ 访问体验质量标准 (SLO 分级标尺)</div>
  <div style="display:flex;height:24px;border-radius:2px;overflow:hidden;margin-top:8px;font-size:11px;color:#FFF;font-weight:bold;text-align:center;line-height:24px;">
    <div style="flex:4;background:#12A679;">● 优秀 (< 50ms)</div>
    <div style="flex:3;background:#52C41A;">● 良好 (50~100ms)</div>
    <div style="flex:2;background:#FA8C16;">● 卡慢预警 (100~300ms)</div>
    <div style="flex:1;background:#D9363E;">● 严重 (>= 300ms)</div>
  </div>
</div>
```

---

## 四、左右两栏排障架构线框模版 (Two-Column Layout)

对于像 `DEM-用户详情.html` 的复杂排障场景，线框图必须忠实表达其两栏架构：

```html
<div class="wf-row" style="align-items:stretch;min-height:360px;">
  <!-- 左侧: 240px 应用列表 (支持筛选与折叠) -->
  <div style="width:240px;background:#FFF;border:1px solid #E1E5EB;border-radius:2px;padding:10px;display:flex;flex-direction:column;gap:8px;flex-shrink:0;">
    <div style="display:flex;justify-content:space-between;align-items:center;">
      <span style="font-size:12px;font-weight:bold;">应用访问列表</span>
      <span style="font-size:11px;color:#1C6EFF;cursor:default;">全部应用 ▾</span>
    </div>
    <input style="height:24px;border:1px solid #CBD5E1;padding:0 6px;font-size:11px;" placeholder="搜索名称/地址" />
    <div style="flex:1;border:1px solid #F1F5F9;background:#FAFBFD;padding:6px;font-size:11px;display:flex;flex-direction:column;gap:4px;">
      <div style="padding:4px 6px;background:#E8F4FF;border:1px solid #BAE6FD;border-radius:2px;font-weight:bold;">
        ● OA 协同系统 <span class="tag" style="float:right;background:#FFF1F0;color:#D9363E;border-color:#FFA39E;">差</span>
      </div>
      <div style="padding:4px 6px;background:#FFF;border:1px solid #E2E8F0;border-radius:2px;">
        ● Salesforce CRM <span class="tag" style="float:right;background:#FFFBE6;color:#FA8C16;border-color:#FFE58F;">一般</span>
      </div>
      <div style="padding:4px 6px;background:#FFF;border:1px solid #E2E8F0;border-radius:2px;">
        ● 企业 ERP <span class="tag" style="float:right;background:#F6FFED;color:#12A679;border-color:#B7EB8F;">正常</span>
      </div>
    </div>
  </div>

  <!-- 右侧: 主排障工作台 (拓扑链 + 散点图 + 根因卡片 + Hop追踪) -->
  <div style="flex:1;min-width:0;display:flex;flex-direction:column;gap:10px;">
    <!-- 拓扑链组件 -->
    <div class="wf-card">🌐 端到端 5 节点网络诊断拓扑链</div>
    <!-- 散点时间线组件 -->
    <div class="wf-card">📊 离散采样体验散点时间线</div>
    <!-- Hop 详细追踪表格 -->
    <div class="wf-table">
      <div class="wf-th">
        <span style="width:10%;">Hop</span>
        <span style="width:25%;">节点 IP</span>
        <span style="width:25%;">ISP / ASN 属性</span>
        <span style="width:20%;">地区</span>
        <span style="width:20%;">RTT (较上一跳)</span>
      </div>
      <div class="wf-tr">
        <span style="width:10%;">1</span>
        <span style="width:25%;">10.20.1.1</span>
        <span style="width:25%;">局域网网关</span>
        <span style="width:20%;">本地内网</span>
        <span style="width:20%;">0.8ms</span>
      </div>
    </div>
  </div>
</div>
```

---

## 五、侧滑抽屉与表单规范 (Drawer & Form Item)

```html
<!-- 抽屉线框：严格遮罩 + 右侧滑出面板 -->
<div class="wf-drawer-overlay">
  <div class="wf-drawer-body" style="width:480px;">
    <div class="wf-header">
      <span>配置探测策略</span>
      <span style="cursor:default;color:#6F7785;">✕</span>
    </div>
    
    <!-- 表单项：严格遵循左 Label 右 Control 左右排版 -->
    <div class="wf-form-item">
      <div class="wf-form-label"><span style="color:#D9363E;">*</span> 策略名称：</div>
      <div class="wf-form-control">
        <input style="width:100%;height:28px;border:1px solid #CBD5E1;padding:0 8px;font-size:11px;" value="核心 OA 拨测策略" />
      </div>
    </div>

    <div class="wf-form-item">
      <div class="wf-form-label"><span style="color:#D9363E;">*</span> 探测频率：</div>
      <div class="wf-form-control">
        <span style="display:inline-block;width:100%;height:28px;border:1px solid #CBD5E1;background:#FFF;padding:4px 8px;font-size:11px;">每 1 分钟 ▾</span>
      </div>
    </div>

    <!-- 底部操作条 -->
    <div style="margin-top:auto;display:flex;justify-content:flex-end;gap:8px;padding-top:16px;border-top:1px solid #E2E8F0;">
      <span class="wf-btn">取消</span>
      <span class="wf-btn-primary">保存策略</span>
    </div>
  </div>
</div>
```
