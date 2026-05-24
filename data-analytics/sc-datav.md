# SC DataV

- **地址**：https://github.com/knight-L/sc-datav
- **作者**：knight-L
- **协议**：Apache-2.0
- **分类**：数据分析与可视化

## 简介

基于 Three.js + React 19 + ECharts 的 3D 地图可视化大屏项目。以四川省地理轮廓为基础，实现精确的 3D 地图渲染、轮廓飞线动画、侧边扫光效果，配合多种 ECharts 图表联动，构建完整的数据大屏展示方案。

## 核心特性

- **3D 地图渲染**：基于 Three.js 的 3D 地图，支持地理轮廓精确呈现、飞线动画、侧边扫光等视觉效果
- **省级地图展示**：以四川省地理数据为示例，提供完整的 GeoJSON 地图数据
- **多图表联动**：柱状图、折线图等多种 ECharts 数据可视化形式与大屏联动
- **响应式设计**：基于 autofit.js 实现多种屏幕尺寸自适应
- **实时调试面板**：集成 Leva 调试工具，支持参数实时调整

## 技术栈

| 类别 | 技术 |
|------|------|
| 核心框架 | React 19 + TypeScript |
| 构建工具 | Vite (Rolldown 版本) |
| 3D 可视化 | Three.js + @react-three/fiber + @react-three/drei |
| 数据图表 | ECharts |
| 地理数据处理 | D3-geo |
| 动画库 | GSAP |
| 样式方案 | Styled-components |
| 调试工具 | Leva |
| 自适应布局 | autofit.js |

## 项目结构

```
src/
├── assets/             # 静态资源（GeoJSON 地图数据）
├── components/         # 通用组件（图表、虚拟滚动）
├── hooks/              # 自定义 Hooks
├── pages/SCDataV/      # 数据大屏页面（地图、飞线、图表）
└── App.tsx             # 应用入口
```

## 安装与使用

```bash
# 安装依赖（需要 Node.js >= 18, PNPM >= 8）
pnpm install

# 开发运行
pnpm dev

# 构建部署
pnpm build && pnpm preview
```

## 亮点 / 个人评价

这个项目是一个完整的 3D 可视化大屏实战案例，技术栈选型现代（React 19 + Three.js + ECharts）。对于需要开发类似数据大屏的开发者来说，3D 地图渲染、飞线动画、多图表联动等功能的实现方式都有很好的参考价值。项目还配套了地图轮廓贴图下载工具（sat-hunter），方便获取其他省份的地理数据。
