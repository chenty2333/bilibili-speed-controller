# Bilibili 自定义倍速控制器

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![UserScript](https://img.shields.io/badge/UserScript-Tampermonkey-green.svg)](https://www.tampermonkey.net/)
[![Version](https://img.shields.io/badge/Version-1.0.0-blue.svg)]()

一款为 Bilibili 设计的高度可定制视频倍速控制脚本，提供可拖动的悬浮控件，增强原生倍速功能，让你的观看体验更加便捷。

## ✨ 主要功能

### 🎯 核心特性
- **自定义倍速列表** - 完全自定义支持的播放倍速，不受原生限制
- **可拖动控件** - 悬浮控件可自由拖动，记忆位置
- **智能隐藏** - 全屏/窗口模式下智能自动隐藏，不干扰观看
- **原生同步** - 与 Bilibili 原生倍速菜单双向同步
- **位置记忆** - 控件位置自动保存，下次访问恢复

### 🛡️ 用户体验
- **Hover 防隐藏** - 鼠标悬停时暂停自动隐藏
- **拖动分隔** - 专用拖动区域，避免误触按钮
- **快速切换** - 一键切换常用倍速
- **设置面板** - 直观的设置界面，实时编辑倍速列表

## 🚀 安装使用

### 前置要求
- 浏览器扩展：[Tampermonkey](https://www.tampermonkey.net/) 或其他支持 UserScript 的扩展
- 支持网站：Bilibili 视频页面

### 安装步骤
1. 安装 Tampermonkey 浏览器扩展
2. 下载 `bilibili-speed-controller.user.js` 文件
3. 在 Tampermonkey 管理面板中导入脚本，或直接打开 `.user.js` 文件安装
4. 访问任意 Bilibili 视频页面即可看到悬浮控件

### 支持页面
- `https://www.bilibili.com/video/*` - 普通视频
- `https://www.bilibili.com/bangumi/*` - 番剧动漫
- `https://www.bilibili.com/list/*` - 播放列表
- `https://www.bili-s.com/video/*` - 备用域名

## 🎮 使用说明

### 控件界面
控件由三部分组成：
- **当前倍速按钮** - 显示当前倍速，点击弹出倍速菜单
- **拖动分隔条** - 专用拖动区域（宽度 16px）
- **设置按钮** - 齿轮图标，点击打开设置面板

### 基本操作
1. **切换倍速**：点击当前倍速按钮，从弹出菜单选择
2. **拖动位置**：在拖动分隔条区域按住鼠标拖动
3. **自定义倍速**：点击设置按钮，编辑倍速列表
4. **重置位置**：在设置面板中点击"重置位置"

### 智能隐藏机制
- **窗口模式**：600ms 无鼠标活动后自动隐藏
- **全屏模式**：3000ms 无鼠标活动后自动隐藏
- **启动保护**：页面加载后 2000ms 内不会隐藏
- **悬停保护**：鼠标悬停在控件上时暂停隐藏

## ⚙️ 配置选项

### 默认配置
```javascript
speeds: [0.5, 1, 1.25, 1.5, 2]  // 默认倍速列表
current: 1                        // 默认倍速
pos: { xPct: null, yPct: null }   // 控件位置（null = 右上角）
```

### 自定义倍速
在设置面板中输入倍速值，支持格式：
- 逗号分隔：`0.75, 1, 1.25, 1.5, 2, 2.5`
- 中文逗号：`0.75，1，1.25，1.5，2`
- 空格分隔：`0.75 1 1.25 1.5 2`

### 时间配置
可在代码中修改以下常量：
```javascript
WINDOW_HIDE_MS = 600      // 窗口模式隐藏延迟
FULLSCREEN_HIDE_MS = 3000 // 全屏模式隐藏延迟
STARTUP_GRACE_MS = 2000   // 启动保护时间
DRAG_HANDLE_WIDTH = 16    // 拖动条宽度
```

## 🔧 技术特性

### 存储机制
- 优先使用 `GM_getValue/GM_setValue`（Tampermonkey API）
- 降级使用 `localStorage`（普通浏览器存储）
- 存储键名：`bili_custom_speed_store_v8`

### 兼容性处理
- **多种播放器**：支持新旧版播放器界面
- **Shadow DOM**：兼容 `bwp-video` 组件
- **SPA 路由**：监听页面变化，自动重新绑定
- **全屏检测**：监听全屏状态变化

### 性能优化
- **防抖处理**：页面变化检测有 200ms 防抖
- **事件绑定**：防止重复绑定，提高性能
- **DOM 观察**：使用 MutationObserver 监听 DOM 变化

## 🛠️ 开发信息

### 技术栈
- 纯 JavaScript（ES6+）
- UserScript API（Tampermonkey）
- DOM API + CSS3

### 代码结构
```
├── 配置选项和默认值
├── 存储管理（GM_API + localStorage）
├── DOM 辅助函数
├── 样式定义（GM_addStyle）
├── UI 构建和事件绑定
├── 拖拽和位置管理
├── 倍速控制核心
├── 原生菜单同步
├── SPA 路由监听
└── 初始化流程
```

### 调试模式
脚本包含详细的控制台日志，前缀为 `[BiliSpeed]`，方便调试和问题排查。

## 📝 更新日志

### v1.0.0
- ✅ 实现自定义倍速列表功能
- ✅ 添加可拖动悬浮控件
- ✅ 支持智能自动隐藏
- ✅ 实现原生倍速双向同步
- ✅ 添加位置记忆功能
- ✅ 支持 Hover 防隐藏
- ✅ 添加拖动分隔区域

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！

### 开发环境
1. Fork 本仓库
2. 在本地修改 `bilibili-speed-controller.user.js`
3. 在 Tampermonkey 中测试
4. 提交 Pull Request

### 问题反馈
如遇到问题，请提供：
- 浏览器版本和 Tampermonkey 版本
- 具体的错误现象或截图
- 浏览器控制台的错误信息

## 📄 许可证

本项目采用 [MIT 许可证](LICENSE)。

## 👨‍💻 作者

**cty2333** - [GitHub](https://github.com/chenty2333)

---

⭐ 如果这个项目对你有帮助，欢迎给个 Star！
