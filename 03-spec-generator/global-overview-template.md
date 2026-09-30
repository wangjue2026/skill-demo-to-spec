# 全局总控说明书模板 (Global Overview Template)

> 💡 **定位**：
> 当一个复杂方案（如方案七）触发了「1 + N 分册规约」时，本模板专门用于生成**第 0 号"全局总控"说明书** (`00-[方案名]-全局架构与路由拓扑.html`)。
>
> **与分册模板（spec-template.md）的本质区别**：
> - **总控只管"全局骨架与流转"**：页面清单大表、Mermaid 系统级拓扑、跨页参数协议。
> - **总控不含任何线框图**：具体页面的线框图、组件映射清单、状态机规则全部交由各独立分册承载。
> - **总控是"施工总指挥"**：它的核心价值是让研发一眼看清整个方案包含哪几个分册、各分册之间的数据流和路由关系是什么。

---

## 骨架模板（HTML 形式）

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>[方案名] 全局架构与路由拓扑 - 总控说明书</title>
  <style>
    :root {
      --bg: #F7F9FC; --card: #FFFFFF; --border: #E1E5EB;
      --text: #2F3540; --text-sub: #6F7785;
      --blue: #1C6EFF; --blue-l: #E8F4FF; --blue-border: #BAE6FD;
      --green-t: #12A679; --green-b: #F6FFED; --green-bd: #B7EB8F;
      --warn-t: #FA8C16; --warn-b: #FFFBE6; --warn-bd: #FFE58F;
      --danger-t: #D9363E; --danger-b: #FFF1F0; --danger-bd: #FFA39E;
    }
    * { box-sizing: border-box; }
    body {
      margin: 0; background: var(--bg); color: var(--text);
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif;
      font-size: 13px; line-height: 1.7;
    }
    .wrap { max-width: 1120px; margin: 0 auto; padding: 24px; }
    .doc { background: var(--card); border: 1px solid var(--border); border-radius: 6px; padding: 36px; box-shadow: 0 1px 3px rgba(15,23,42,0.04); }
    h1 { font-size: 22px; line-height: 30px; font-weight: 700; margin: 0 0 16px; color: #1E293B; }
    h2 { font-size: 16px; line-height: 24px; font-weight: 600; margin: 36px 0 14px; padding-bottom: 8px; border-bottom: 1px solid var(--border); color: #1E293B; }
    h3 { font-size: 14px; font-weight: 600; margin: 24px 0 10px; color: #2F3540; }

    .meta { color: var(--text-sub); font-size: 12px; margin-bottom: 24px; line-height: 2; background: #F8FAFC; padding: 12px 16px; border-radius: 4px; border: 1px solid var(--border); }
    .meta b { color: var(--text); }
    .status { display: inline-block; padding: 2px 8px; border-radius: 2px; background: var(--green-b); color: var(--green-t); border: 1px solid var(--green-bd); font-size: 11px; font-weight: 500; }

    table { width: 100%; border-collapse: collapse; margin: 12px 0; font-size: 12px; }
    th { background: #EDF1F7; color: #454C59; font-weight: 500; text-align: left; height: 32px; padding: 0 12px; border-bottom: 1px solid var(--border); white-space: nowrap; }
    td { height: 38px; padding: 6px 12px; border-bottom: 1px solid var(--border); vertical-align: top; }

    .tag { display: inline-block; padding: 1px 8px; border-radius: 2px; font-size: 11px; background: var(--blue-l); color: var(--blue); border: 1px solid var(--blue-border); }
    .tag-spec { display: inline-block; padding: 2px 8px; border-radius: 2px; font-size: 11px; background: #EEF2FF; color: #4F46E5; border: 1px solid #C7D2FE; font-weight: 600; }
    .note { background: #F8FAFC; border: 1px solid var(--border); border-left: 3px solid var(--blue); padding: 8px 12px; margin: 10px 0; font-size: 12px; color: var(--text-sub); }

    /* 纯内嵌离线拓扑流卡片体系 (Zero CDN) */
    .topology-card { background: #FAFBFD; border: 1px solid #CBD5E1; border-radius: 6px; padding: 20px; margin: 16px 0; }
    .node-chain { display: flex; align-items: center; justify-content: space-between; gap: 8px; flex-wrap: wrap; margin: 14px 0; }
    .node-box { background: #FFFFFF; border: 1px solid #CBD5E1; border-radius: 4px; padding: 12px 14px; min-width: 150px; text-align: center; box-shadow: 0 1px 2px rgba(0,0,0,0.03); }
    .node-title { font-weight: 600; color: #1E293B; margin-bottom: 4px; }
    .node-desc { font-size: 11px; color: var(--text-sub); }
    .arrow-icon { color: var(--blue); font-weight: bold; font-size: 13px; }
    .mermaid-source { background: #F8FAFC; border: 1px solid var(--border); border-radius: 4px; padding: 12px; margin: 10px 0; font-family: ui-monospace, monospace; font-size: 11px; color: #334155; overflow-x: auto; }

    .checkpoint { background: var(--blue-l); border: 1px solid #BAE6FD; border-radius: 4px; padding: 16px 20px; margin-top: 36px; font-size: 12px; color: #1C6EFF; line-height: 1.8; }
    .checkpoint b { display: block; margin-bottom: 6px; font-size: 13px; color: #1C6EFF; }
  </style>
</head>
<body>
<div class="wrap">
  <div class="doc">
    <h1>🏗️ [方案名] 全局架构与路由拓扑 · 总控说明书</h1>
    <div class="meta">
      <b>方案生成模式</b>：原型逆向工程 (demo-to-spec 提纯) · 1 + N 分册总控<br/>
      <b>原始 Demo 来源</b>：<code>[方案目录路径，如：Demos/07-方案七/]</code><br/>
      <b>技术栈对齐</b>：Vue 3 + IDUX (@idux/components) + Common Design 内部平台标准<br/>
      <b>面向对象</b>：内部平台研发团队 / 前端架构师<br/>
      <b>状态</b>：<span class="status">✅ 全局总控就绪 · 各分册按需独立交付</span>
    </div>

    <!-- ==================== 一、方案全景页面清单与职责划分 ==================== -->
    <h2>一、方案全景页面清单与职责划分</h2>

    <h3>1. 所有页面/视图/抽屉清单</h3>
    <table>
      <thead>
        <tr>
          <th style="width:10%;">页面编号</th>
          <th style="width:22%;">页面 / 视图名称</th>
          <th style="width:12%;">交互形态</th>
          <th style="width:18%;">选用页面模板</th>
          <th style="width:20%;">核心职责</th>
          <th style="width:18%;">归属分册</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><b>Page-01</b></td>
          <td>[首页/大盘名称]</td>
          <td>主页面 (Page)</td>
          <td><code>page-table-overview</code></td>
          <td>[职责描述]</td>
          <td><span class="tag">spec-01</span></td>
        </tr>
        <tr>
          <td><b>Page-02</b></td>
          <td>[详情/排障页面名称]</td>
          <td>主页面 (Page)</td>
          <td><code>page-detail-master</code></td>
          <td>[职责描述]</td>
          <td><span class="tag">spec-02</span></td>
        </tr>
        <tr>
          <td><b>Drawer-01</b></td>
          <td>[排障抽屉名称]</td>
          <td>右侧抽屉 (Drawer)</td>
          <td><code>page-form-drawer</code></td>
          <td>[职责描述]</td>
          <td><span class="tag">spec-02</span></td>
        </tr>
      </tbody>
    </table>

    <h3>2. 业务分册与源 HTML 原型 1:1 镜像映射大表</h3>
    <div class="note">
      <b>⚠️ 信息架构保真铁律</b>：源方案包含几个独立的 HTML 原型文件，就必须严格输出几个独立的业务分册（1 HTML = 1 Spec）！绝对禁止跨页面合并归类，彻底保真系统级路由与信息架构！
    </div>
    <table>
      <thead>
        <tr>
          <th style="width:14%;">分册编号</th>
          <th style="width:20%;">分册主题名称</th>
          <th style="width:22%;">对应源 HTML 原型</th>
          <th style="width:20%;">选用页面模板</th>
          <th style="width:24%;">核心组件与特化资产</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><span class="tag-spec">spec-01</span></td>
          <td><b>全网体验监控大盘</b></td>
          <td><code>DEM-首页.html</code></td>
          <td><code>30%:40%:30% 综合概览</code></td>
          <td>IxCard, IxTable, 双层 AI 抽屉</td>
        </tr>
        <tr>
          <td><span class="tag-spec">spec-02</span></td>
          <td><b>全网体验预警中心</b></td>
          <td><code>DEM-体验预警.html</code></td>
          <td><code>page-table-overview</code></td>
          <td>132px 预警大盘, 10 列表格, 策略抽屉</td>
        </tr>
        <tr>
          <td><span class="tag-spec">spec-03</span></td>
          <td><b>用户全链路排障定位</b></td>
          <td><code>DEM-用户详情.html</code></td>
          <td><code>两栏排障定制模板</code></td>
          <td>240px 侧栏, 5 节点拓扑链, 散点时间线</td>
        </tr>
        <tr>
          <td><span class="tag-spec">spec-04</span></td>
          <td><b>应用体验与关联分析</b></td>
          <td><code>DEM-应用详情.html</code></td>
          <td><code>page-detail-drilldown</code></td>
          <td>时序走势, 4 张洞察卡片, 分支/用户双 Tab</td>
        </tr>
        <tr>
          <td><span class="tag-spec">spec-05</span></td>
          <td><b>监控与探测配置中心</b></td>
          <td><code>DEM-监控配置.html</code></td>
          <td><code>定制复合配置模板</code></td>
          <td>资产大盘, 9 列自定义明细表, 探测任务</td>
        </tr>
      </tbody>
    </table>

    <!-- ==================== 二、系统级路由拓扑 ==================== -->
    <h2>二、系统级路由拓扑与页面流转</h2>

    <h3>1. 全局流转拓扑架构 (纯 HTML/CSS 离线节点流 · 100% Zero CDN)</h3>
    <div class="topology-card">
      <div class="node-chain">
        <div class="node-box" style="border-top: 3px solid #1C6EFF;">
          <div class="node-title">spec-01: 首页大盘</div>
          <div class="node-desc">感知全网体验波动<br/>锁定 VIP 劣化对象与异常</div>
        </div>
        <div class="arrow-icon">➔ 下钻排障 ➔</div>
        <div class="node-box" style="border-top: 3px solid #FA8C16;">
          <div class="node-title">spec-02 / 03: 详情与排障</div>
          <div class="node-desc">5 节点诊断拓扑链<br/>三色散点标尺定界分析</div>
        </div>
        <div class="arrow-icon">➔ 联动追查 ➔</div>
        <div class="node-box" style="border-top: 3px solid #12A679;">
          <div class="node-title">spec-04 / 05: 关联与配置</div>
          <div class="node-desc">时序质量趋势回溯<br/>调整拨测阈值与策略</div>
        </div>
      </div>
      <div class="node-chain" style="margin-top: 20px;">
        <div class="node-box" style="border-left: 3px solid #1C6EFF; text-align: left; flex: 1;">
          <div class="node-title">侧滑抽屉 (Drawer) 联动动线</div>
          <div class="node-desc">行操作点击【详情】或【排障】 ➔ 受控滑出 640px 独立抽屉 ➔ 传递单点实体上下文 ➔ 关闭抽屉回写状态</div>
        </div>
      </div>
    </div>

    <div class="note">
      💡 <b>可选 Mermaid DSL 原生拓扑源码</b>（供复制到 Markdown / Obsidian 查看）：
    </div>
    <div class="mermaid-source">
graph TD
  classDef page fill:#E8F4FF,stroke:#1C6EFF,stroke-width:1.5px,color:#1C6EFF;
  classDef drawer fill:#F6FFED,stroke:#12A679,stroke-width:1.5px,color:#12A679;
  Root["产品基座 · 一级导航"] --> P1["首页大盘 (Page)"]:::page
  Root --> P2["用户详情/排障页 (Page)"]:::page
  P1 -->|"点击行操作"| D1["诊断抽屉 (IxDrawer)"]:::drawer
  P1 -->|"下钻跳转"| P2
    </div>

    <h3>2. 跨页面参数传递协议</h3>
    <table>
      <thead>
        <tr>
          <th style="width:18%;">源页面</th>
          <th style="width:18%;">目标页面</th>
          <th style="width:16%;">传递方式</th>
          <th style="width:24%;">参数字段</th>
          <th style="width:24%;">说明</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Page-01 首页</td>
          <td>Page-02 用户详情</td>
          <td>URL Query</td>
          <td><code>?userId=xxx&timestamp=xxx</code></td>
          <td>点击首页用户列表行跳转至用户详情排障页</td>
        </tr>
        <tr>
          <td>Page-01 首页</td>
          <td>Drawer-01 应用诊断</td>
          <td>组件 Props / Pinia</td>
          <td><code>appId: string</code></td>
          <td>点击行操作按钮打开右侧抽屉</td>
        </tr>
      </tbody>
    </table>

    <div class="note">
      💡 <b>Vue Router 路由规划提示</b>：每个 Page 对应 Vue Router 路由表中的一个独立 <code>path</code>；Drawer 与 Modal 不设独立路由，通过所属页面的响应式状态控制。
    </div>

    <!-- 底部研发施工确认关卡 -->
    <div class="checkpoint">
      <b>🚦 总控施工指引 (Engineering Guide)</b>
      本文件是方案全局总控，具体页面施工请按分册编号查阅对应分册说明书：<br/>
      1. <b>分册 spec-01</b>：[监控大盘与体验预警] — 查看线框图与 IDUX 组件映射。<br/>
      2. <b>分册 spec-02</b>：[深度排障定位中心] — 查看时序图表与诊断链路线框。<br/>
      3. <b>分册 spec-03</b>：[探测任务与监控配置] — 查看表单向导与规则配置线框。
    </div>

  </div>
</div>
</body>
</html>
```
