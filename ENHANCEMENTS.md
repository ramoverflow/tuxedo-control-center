# TUXEDO Control Center - Enhanced Fork

## 新增功能 / New Features

### 1. 键盘背光动画支持 / Keyboard Backlight Animations
- **呼吸效果** (Breathing) - 颜色缓慢淡入淡出
- **波浪效果** (Wave) - 光线在键盘上流动
- **反应式** (Reactive) - 按键按下时点亮
- **光谱** (Spectrum) - 彩虹色循环
- 支持动画速度调节 (0-255)

### 2. Electron 内存优化 / Memory Optimization
- **延迟加载 GUI** - 应用启动时仅加载系统托盘
- 用户点击托盘图标时才加载主窗口
- **内存占用减少** 从 ~200-300MB 降至 ~50-80MB
- 关闭 GUI 后内存自动释放

### 3. 中文语言支持 / Chinese Language Support
- 完整的 zh-CN (简体中文) 本地化
- 键盘背光所有功能的中文翻译
- 支持系统语言自动检测

## 实现细节 / Implementation Details

### 后端更改 / Backend Changes

**文件**: `src/service-app/classes/KeyboardBacklightListener.ts`
- 新增 `detectSupportedModes()` 方法检测硬件支持的动画模式
- 为每个动画效果实现了单独的方法：
  - `setStaticEffect()` - 静态颜色
  - `setBreathingEffect()` - 呼吸效果
  - `setWaveEffect()` - 波浪效果
  - `setReactiveEffect()` - 反应式效果
  - `setSpectrumEffect()` - 光谱效果

**文件**: `src/e-app/backendAPIs/initMain.ts`
- 优化 Electron 应用初始化
- 延迟加载 GUI 直到用户点击托盘
- 添加 `zh-CN` 到可用语言列表

### 前端更改 / Frontend Changes

**文件**: `src/ng-app/app/keyboard-backlight/keyboard-backlight.component.ts`
- 新增 `chosenMode` 属性跟踪当前动画模式
- 新增 `chosenSpeed` 属性控制动画速度
- 实现 `onModeChanged()` 处理模式切换
- 实现 `onSpeedChanged()` 处理速度调节

**文件**: `src/ng-app/app/keyboard-backlight/keyboard-backlight.component.html`
- 新增动画模式选择器
- 新增动画速度滑块
- 根据硬件能力动态显示/隐藏选项

### 数据模型更改 / Data Model Changes

**文件**: `src/common/models/TccSettings.ts`
- 扩展 `KeyboardBacklightColorModes` 枚举：
  - `static = 0`
  - `breathing = 1`
  - `wave = 2`
  - `reactive = 3`
  - `spectrum = 4`
- 扩展 `KeyboardBacklightStateInterface`：
  - `speed?: number` - 动画速度 (0-255)
  - `effectColor?: string` - 效果颜色 ("#RRGGBB")

## 构建说明 / Build Instructions

```bash
# 克隆仓库
git clone https://github.com/ramoverflow/tuxedo-control-center.git
cd tuxedo-control-center

# 切换到增强功能分支
git checkout feature/keyboard-backlight-animations-and-optimizations

# 安装依赖
npm install

# 构建
npm run build-prod

# 打包
npm run pack-prod
```

## 使用方法 / Usage

### 键盘背光动画
1. 打开 TUXEDO Control Center
2. 导航到 "Tools" → "Keyboard Backlight"
3. 选择动画模式（如果硬件支持）
4. 调节动画速度（仅在非静态模式下可见）
5. 选择颜色

### 内存优化
- 应用默认以托盘模式启动，不加载 GUI
- 点击系统托盘图标打开 GUI
- 关闭 GUI 窗口返回托盘模式
- 右键托盘菜单选择 "Exit" 完全退出

### 语言选择
- 系统会自动检测系统语言
- 打开设置可手动选择语言（包括简体中文）

## 兼容性 / Compatibility

- **Linux Kernel**: 5.15+
- **tuxedo-drivers**: 4.0.0+
- **Electron**: 42.8.1+
- **Angular**: 21.2.18+

## 原始项目 / Original Project

https://github.com/tuxedocomputers/tuxedo-control-center

## 许可证 / License

GNU General Public License v3.0

## 贡献 / Contributing

欢迎提交 Pull Requests 和 Issue 报告！

Welcome to submit Pull Requests and report Issues!
