# TOURGUIDE-WITH-HTML

---
name: html-tour guide
description: Generate a minimal mobile-first offline HTML travel guide from a route, with collapsible destination cards and direct map navigation.
version: 1.0.0
metadata:
  openclaw:
    emoji: "🗺️"
    homepage: https://github.com/otislook/html-tourguide
---


## 目的

将旅行路线转换为一个极简、移动端优先、可离线浏览的 HTML 导览页。

这个 Skill 的目标不是生成一篇很长的旅游攻略，而是帮助旅行者减少 App 切换、信息噪音和操作负担。它会把一条路线整理成一个轻量的手机导览助手：打开页面即可查看总览、浏览路线、展开目的地详情，并通过一个“导航”按钮尽量直接唤起地图导航。

最终成品应该像一个安静、克制、清晰的移动端导览卡片，而不是一个复杂的旅游网站。

---

## 核心定位

这个 Skill 适合用于：

* 整理已经规划好的旅行路线
* 制作轻量级 City Walk 导览页
* 将主题路线转化为手机 HTML 页面
* 与朋友、家人分享路线
* 减少在备忘录、截图、地图 App、文档之间来回切换
* 制作可离线打开的自助导览工具

这个 Skill 可以辅助优化路线，但核心输出是一个 HTML 导览网页。

---

## 设计理念

### 1. 默认极简

默认界面只展示旅行者当下最需要的信息：

* 这条路线是什么
* 下一站去哪
* 如何打开地图导航

更多内容应当默认收起，用户需要时再点击展开。

---

### 2. Apple-like 视觉风格

最终 HTML 页面应当具有简洁、安静、有质感的视觉体验。

设计风格参考 Apple Notes、Apple Maps、iOS 卡片界面：

* 浅灰白背景
* 白色圆角卡片
* 大留白
* 系统字体
* 轻边框
* 极弱阴影
* 清晰的文字层级
* 克制的颜色使用
* 简洁的按钮样式

避免：

* 复杂渐变
* 大量装饰图片
* 复杂导航栏
* 过多 emoji
* 密集信息块
* 强烈的旅游 App 风格
* 长篇大论式景点介绍

---

### 3. 给观察留下空间

不要过度解释每个地点。

好的导览页应该提供足够的背景，但不替用户完成全部思考。它应该给出简洁的上下文和观察关键词，让旅行者在现场自己观察、联想和判断。

---

## 适用场景

当用户想要完成以下任务时，可以使用本 Skill：

* 把旅行计划变成 HTML 导览页
* 整理一日游路线
* 制作城市漫步路线
* 为每个目的地添加地图导航按钮
* 生成适合手机打开的离线页面
* 分享一条简洁路线给他人
* 制作主题旅行、自助导览或读书旅行路线

典型场景包括：

* 书籍主题路线
* 历史城市路线
* 博物馆路线
* 街区漫步路线
* 美食路线
* 建筑观察路线
* 电影取景地路线
* 社会观察型 City Walk

---

## 输入信息

用户可能提供以下信息：

```yaml
title:
city:
duration:
transportation:
route_theme:
navigation_profile:
stops:
  - name:
    map_keyword:
    summary:
    context:
    observe:
    lat:
    lon:
    coord_type:
    nav_mode:
```

当信息缺失时，可以根据上下文合理补全。

除非缺失信息会导致无法生成可用页面，否则不要频繁追问用户。

---

## 推荐数据结构

在生成 HTML 前，建议先整理成以下结构：

```yaml
guide:
  title: "路线标题"
  theme: "一句话主题"
  city: "城市名称"
  duration: "1 天"
  transportation: "地铁 + 步行"
  route_summary: "地点 A → 地点 B → 地点 C"
  navigation_profile: "auto"

stops:
  - name: "目的地名称"
    map_keyword: "城市 + 目的地名称"
    summary: "一句话说明为什么来这里。"
    context: "简短背景介绍，建议 80-150 字以内。"
    observe:
      - "观察关键词 1"
      - "观察关键词 2"
      - "观察关键词 3"
      - "观察关键词 4"
    lat: 39.849321
    lon: 116.398456
    coord_type: "gcj02"
    nav_mode: "walk"
```

保持数据结构简单。

默认不要加入以下字段：

* long_description
* photo_tips
* packing_list
* detailed_history
* complex_score
* excessive_recommendations

这些内容只有在用户明确要求时才添加。

---

## 内容规则

### 总览部分

总览部分只保留最关键的信息：

* 导览标题
* 一句话主题
* 城市
* 时长
* 交通方式
* 路线顺序

示例：

```text
《浙江村》北京南城一日游

一条关于流动人口、服装市场与城市更新的南城路线。

城市：北京
时长：1 天
交通：地铁 + 步行
路线：大红门 → 海户屯 → 东罗园 → 石榴庄 → 大栅栏 → 天桥
```

总览要简洁，不要写成长篇攻略开头。

---

### 目的地内容

每个目的地包含：

1. 目的地名称
2. 导航按钮
3. 一句话说明
4. 简短背景
5. 观察关键词

默认收起状态：

```text
大红门                                      导航
```

展开状态：

```text
大红门                                      导航

服装批发网络的核心节点，也是理解浙江村经济结构的入口。

这里曾是北京南城服装批发与加工网络的重要区域。沿着街区行走，可以观察市场、物流、居住空间与城市更新之间的关系。

观察：
批发市场 / 物流 / 南城街区 / 产业迁移
```

---

### 文案风格

语言应当简洁、克制、平静，偏观察型。

推荐写法：

```text
服装批发网络的核心节点。
```

不推荐写法：

```text
这里是一个非常值得你认真观察和深入思考的地方，因为它充分体现了中国改革开放以来城市化进程中的复杂社会变迁……
```

推荐使用：

* 路线
* 观察
* 街区
* 节点
* 线索
* 变化
* 迁移
* 更新
* 现场
* 痕迹

避免过度使用：

* 你必须
* 你一定要
* 非常重要
* 深入思考
* 充分体现
* 极具代表性
* 不容错过

---

## HTML 输出要求

生成一个单文件 HTML。

HTML 应当满足：

* 可保存后离线打开
* 移动端优先
* 不依赖外部 CSS 库
* 不依赖外部 JavaScript 库
* 使用系统字体
* 支持响应式布局
* 每个目的地都有导航按钮
* CSS 与 JavaScript 均写在同一个 HTML 文件内

除用户点击导航按钮和网页地图兜底外，不应依赖外部网络资源。

---

## 页面结构

最终页面默认只包含两个主要部分：

```text
1. 总览
2. 路线列表
```

不要默认添加太多栏目。

例如：

* 延伸阅读
* 摄影建议
* 美食推荐
* 打包清单
* 参考资料

这些只在用户明确要求时添加。

---

## 第一部分：总览

总览部分应当视觉突出，但内容紧凑。

推荐结构：

```text
[导览标题]

[一句话主题]

城市        北京
时长        1 天
交通        地铁 + 步行

路线
地点 A → 地点 B → 地点 C → 地点 D
```

使用卡片布局。

---

## 第二部分：路线列表

路线列表是页面核心。

每个目的地显示为一行可折叠卡片。

### 默认收起状态

每一行只展示：

* 左侧：目的地名称
* 右侧：导航按钮

示例：

```text
大红门                                      导航
海户屯                                      导航
东罗园                                      导航
石榴庄                                      导航
大栅栏                                      导航
天桥                                        导航
```

### 点击展开状态

点击某一行后展示：

* 一句话说明
* 简短背景
* 观察关键词

展开内容必须简短，不要写成长篇文章。

---

## 交互规则

* 点击目的地行，展开或收起详情。
* 点击“导航”按钮，尝试打开地图导航。
* 点击“导航”按钮时，不应触发行展开或收起。
* 默认情况下，同一时间只展开一个目的地。
* 交互应当轻量、快速、无复杂动画。
* 默认不要展示多地图选择面板。

JavaScript 只用于折叠列表和导航唤起处理。

---

## 导航策略

导航体验应当保持简单。

每个目的地只展示一个“导航”按钮。

默认不要展示多地图选择面板。

### 默认导航行为

使用以下设置：

```yaml
navigation_profile: auto
```

可选值：

```yaml
auto:
  Android: 尝试直接唤起高德地图，失败后回退 Google Maps。
  iOS: 先尝试唤起高德地图，失败后回退 Apple 系统地图。
  Other: 打开网页地图兜底。

android_amap_google:
  Android 专用策略。优先尝试高德地图，失败后回退 Google Maps。

ios_amap_system:
  iOS 专用策略。优先尝试高德地图，失败后回退 Apple 系统地图。
```

### 重要限制

普通 HTML 页面不能可靠检测用户手机安装了哪些地图 App，也不能完全绕过 Android 或 iOS 的系统确认弹窗。

导览页应尽量尝试直接唤起地图 App，但系统或浏览器仍可能出现以下情况：

* 弹出确认框
* 先打开浏览器
* 阻止外部 App 唤起
* 回退到网页地图
* 在部分内置浏览器中无响应

这是移动系统和浏览器安全机制导致的正常现象。

---

## 导航数据要求

为了尽量直接进入路线导航，每个目的地最好包含经纬度：

```yaml
stops:
  - name: "目的地名称"
    map_keyword: "城市 + 目的地名称"
    lat: 39.849321
    lon: 116.398456
    coord_type: "gcj02"
    nav_mode: "walk"
```

如果提供了 `lat` 和 `lon`：

* Android 端应尝试打开高德路线规划，失败后回退 Google Maps。
* iOS 端应先尝试打开高德路线规划，失败后回退 Apple 系统地图。

如果缺少经纬度：

* Android 端回退为高德地点搜索，并通过 Google Maps 作为失败兜底。
* iOS 端回退为高德地点搜索，并通过 Apple 系统地图作为失败兜底。

中国大陆路线建议优先使用 GCJ-02 坐标，适配高德地图。

如果坐标不确定，优先使用关键词搜索，避免导航位置偏移。

---

## 地图唤起规则

### Android

Android 端点击导航按钮后，应通过 Android Intent URL 直接尝试唤起高德地图路线规划。

高德地图包名：

```text
com.autonavi.minimap
```

City Walk 默认使用步行模式：

```text
t=2
```

如果用户没有安装高德地图，或高德地图无法被唤起，则 Android Intent 的 `browser_fallback_url` 应回退到 Google Maps。

Android 兜底链接使用 Google Maps 路线规划：

```text
https://www.google.com/maps/dir/?api=1&destination={encoded_destination}&travelmode=walking
```

如果缺少经纬度，则使用目的地关键词：

```text
https://www.google.com/maps/dir/?api=1&destination={encoded_keyword}&travelmode=walking
```

---

### iOS

iOS 端点击导航按钮后，应：

1. 先使用 `iosamap://` URL Scheme 尝试打开高德地图。
2. 如果高德地图没有成功打开，则短暂延迟后回退到 Apple 系统地图。

默认不要展示地图选择器。

---

### 其他设备

使用网页地图兜底。

中国大陆路线可优先使用高德网页地图兜底：

```text
https://uri.amap.com/search?keyword={encoded_keyword}&callnative=1
```

国际路线可根据需要使用 Google Maps 或 Apple Maps 网页链接。

---

## 默认视觉规范

建议使用以下 CSS 变量：

```css
:root {
  --bg: #f5f5f7;
  --card: #ffffff;
  --text: #1d1d1f;
  --muted: #6e6e73;
  --line: rgba(0, 0, 0, 0.08);
  --accent: #007aff;
  --radius: 22px;
}
```

字体：

```css
font-family: -apple-system, BlinkMacSystemFont, "SF Pro Text", "Helvetica Neue", Arial, sans-serif;
```

布局建议：

* 最大宽度：760px
* 移动端边距：18px
* 卡片圆角：20-24px
* 按钮圆角：999px
* 避免强阴影
* 优先使用轻边框
* 行高：1.55-1.7
* 标题清晰，正文克制
* 保持充足留白

---

## 深色模式

建议支持系统深色模式。

示例：

```css
@media (prefers-color-scheme: dark) {
  :root {
    --bg: #000000;
    --card: #1c1c1e;
    --text: #f5f5f7;
    --muted: #a1a1a6;
    --line: rgba(255, 255, 255, 0.12);
    --accent: #0a84ff;
  }
}
```

---

## HTML 结构参考

可使用类似结构：

```html
<div class="stop" data-stop>
  <div class="stop-header">
    <button class="stop-toggle">
      <span class="stop-name">大红门</span>
    </button>
    <button
      class="nav-button"
      onclick='openNavigation({
        name: "大红门",
        map_keyword: "北京 大红门",
        lat: 39.849321,
        lon: 116.398456,
        coord_type: "gcj02",
        nav_mode: "walk"
      }, event)'
    >
      导航
    </button>
  </div>

  <div class="stop-detail">
    <p class="summary">服装批发网络的核心节点。</p>
    <p class="context">这里曾是北京南城服装批发与加工网络的重要区域。</p>
    <div class="keywords">
      <span>批发市场</span>
      <span>物流</span>
      <span>南城街区</span>
      <span>产业迁移</span>
    </div>
  </div>
</div>
```

折叠交互参考：

```javascript
document.querySelectorAll("[data-stop]").forEach((stop) => {
  const toggle = stop.querySelector(".stop-toggle");

  toggle.addEventListener("click", () => {
    document.querySelectorAll("[data-stop]").forEach((item) => {
      if (item !== stop) item.classList.remove("open");
    });
    stop.classList.toggle("open");
  });
});
```

导航唤起逻辑参考：

```javascript
const NAV_PROFILE = "auto";

function enc(value) {
  return encodeURIComponent(value || "");
}

function hasCoord(stop) {
  return stop.lat && stop.lon;
}

function getModeCode(stop) {
  const mode = stop.nav_mode || "walk";
  if (mode === "drive") return "0";
  if (mode === "bus") return "1";
  if (mode === "walk") return "2";
  if (mode === "ride") return "3";
  return "2";
}

function getGoogleTravelMode(stop) {
  const mode = stop.nav_mode || "walk";
  if (mode === "drive") return "driving";
  if (mode === "bus") return "transit";
  if (mode === "walk") return "walking";
  if (mode === "ride") return "bicycling";
  return "walking";
}

function createGoogleMapsFallback(stop) {
  const destination = hasCoord(stop)
    ? stop.lat + "," + stop.lon
    : (stop.map_keyword || stop.name);

  return (
    "https://www.google.com/maps/dir/?" +
    "api=1" +
    "&destination=" + enc(destination) +
    "&travelmode=" + getGoogleTravelMode(stop)
  );
}

function createAmapWebFallback(stop) {
  const keyword = stop.map_keyword || stop.name;

  if (hasCoord(stop)) {
    return (
      "https://uri.amap.com/navigation" +
      "?from=" +
      "&to=" + stop.lon + "," + stop.lat + "," + enc(stop.name) +
      "&mode=walk" +
      "&src=tourguide" +
      "&coordinate=gaode" +
      "&callnative=1"
    );
  }

  return "https://uri.amap.com/search?keyword=" + enc(keyword) + "&callnative=1";
}

function createAndroidAmapRoute(stop) {
  const fallback = encodeURIComponent(createGoogleMapsFallback(stop));

  if (!hasCoord(stop)) {
    return (
      "intent://poi" +
      "?sourceApplication=tourguide" +
      "&keywords=" + enc(stop.map_keyword || stop.name) +
      "&dev=0" +
      "#Intent;" +
      "scheme=androidamap;" +
      "package=com.autonavi.minimap;" +
      "S.browser_fallback_url=" + fallback + ";" +
      "end"
    );
  }

  return (
    "intent://route/plan/" +
    "?sourceApplication=tourguide" +
    "&sid=" +
    "&slat=" +
    "&slon=" +
    "&sname=" + enc("我的位置") +
    "&did=" +
    "&dlat=" + stop.lat +
    "&dlon=" + stop.lon +
    "&dname=" + enc(stop.name) +
    "&dev=0" +
    "&t=" + getModeCode(stop) +
    "#Intent;" +
    "scheme=amapuri;" +
    "package=com.autonavi.minimap;" +
    "S.browser_fallback_url=" + fallback + ";" +
    "end"
  );
}

function createIOSAmapRoute(stop) {
  if (!hasCoord(stop)) {
    return (
      "iosamap://poi" +
      "?sourceApplication=tourguide" +
      "&keywords=" + enc(stop.map_keyword || stop.name) +
      "&dev=0"
    );
  }

  return (
    "iosamap://path" +
    "?sourceApplication=tourguide" +
    "&sid=" +
    "&slat=" +
    "&slon=" +
    "&sname=" + enc("我的位置") +
    "&did=" +
    "&dlat=" + stop.lat +
    "&dlon=" + stop.lon +
    "&dname=" + enc(stop.name) +
    "&dev=0" +
    "&t=" + getModeCode(stop)
  );
}

function createAppleMapsRoute(stop) {
  if (hasCoord(stop)) {
    return (
      "https://maps.apple.com/?" +
      "daddr=" + enc(stop.lat + "," + stop.lon) +
      "&q=" + enc(stop.name) +
      "&dirflg=w"
    );
  }

  return (
    "https://maps.apple.com/?" +
    "daddr=" + enc(stop.map_keyword || stop.name) +
    "&dirflg=w"
  );
}

function openIOSNavigation(stop) {
  const amapUrl = createIOSAmapRoute(stop);
  const appleUrl = createAppleMapsRoute(stop);

  const start = Date.now();

  window.location.href = amapUrl;

  setTimeout(() => {
    const elapsed = Date.now() - start;

    if (elapsed < 1600 && document.visibilityState === "visible") {
      window.location.href = appleUrl;
    }
  }, 900);
}

function openNavigation(stop, event) {
  if (event) {
    event.preventDefault();
    event.stopPropagation();
  }

  const ua = navigator.userAgent || "";
  const isAndroid = /Android/i.test(ua);
  const isIOS = /iPhone|iPad|iPod/i.test(ua);

  if (
    NAV_PROFILE === "android_amap_google" ||
    (NAV_PROFILE === "auto" && isAndroid)
  ) {
    window.location.href = createAndroidAmapRoute(stop);
    return;
  }

  if (
    NAV_PROFILE === "ios_amap_system" ||
    (NAV_PROFILE === "auto" && isIOS)
  ) {
    openIOSNavigation(stop);
    return;
  }

  window.location.href = createAmapWebFallback(stop);
}
```

---

## 质量检查清单

生成 HTML 前，检查以下事项：

* 页面只有两个主要部分：总览、路线列表。
* 每个目的地默认收起。
* 收起状态只展示目的地名和导航按钮。
* 点击目的地行后才展示详情。
* 点击导航按钮会尽量直接打开地图导航。
* 点击导航按钮不会触发展开或收起。
* 默认不展示多地图选择面板。
* Android 端尝试直接唤起高德地图。
* Android 端在高德地图无法打开时回退 Google Maps。
* iOS 端先尝试唤起高德地图。
* iOS 端在高德地图无法打开时回退 Apple 系统地图。
* 每个目的地都有地图关键词。
* 如果可获得坐标，则加入坐标。
* 如果坐标不确定，优先使用关键词搜索。
* 每个目的地的文字足够简洁。
* 没有默认展示长篇攻略。
* 视觉风格简洁、安静、有质感。
* 页面适合手机浏览。
* HTML 为单文件。
* 页面离线可打开。
* 用户能在 10 秒内理解整条路线。

---

## 示例用户请求

```text
请把这条北京路线做成一个极简离线 HTML 导览页：

标题：《浙江村》北京南城一日游
城市：北京
时长：1 天
交通：地铁 + 步行
导航模式：auto
路线：
- 大红门
- 海户屯
- 东罗园
- 石榴庄
- 大栅栏
- 天桥
```

预期输出：

* 一个完整的单文件 HTML
* Apple-like 极简 UI
* 总览部分
* 可折叠路线列表
* 每站一个导航按钮
* Android 端高德地图优先、Google Maps 兜底
* iOS 端高德地图优先、Apple 系统地图兜底
* 简洁的目的地背景
* 观察关键词

---

## 最终输出格式

完成任务时，输出：

1. 生成的 HTML 文件
2. 简短使用说明

示例：

```text
已完成。用手机打开 HTML 文件即可使用。点击目的地行可以展开详情，点击“导航”可以尝试打开地图导航。
```
