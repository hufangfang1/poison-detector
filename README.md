# 二进制编码异常定位工具

基于二进制编码原理，用最少的检测器一次定位异常目标单元。

![演示](poison-detector-final.png)

## 核心原理

N 个检测器代表二进制的 N 位：
- **触发** = 1
- **未触发** = 0

触发结果拼成的二进制数即为异常单元编号。

### 为什么有效？

- 每个目标单元被分配一个唯一的二进制编码
- 每个检测器负责检测对应位为 1 的所有单元
- 触发结果的组合直接指向异常单元的编码

### 效率优势

| 目标单元数 | 所需检测器数 |
|-----------|------------|
| 8         | 3          |
| 16        | 4          |
| 100       | 7          |
| 1024      | 10         |

公式：**检测器数量 = ⌈log₂(n)⌉**

## 功能特性

- 支持 2~1024 个目标单元
- 自动生成检测方案
- 可视化切换检测器状态（触发/未触发）
- 实时定位异常单元
- 显示完整推理过程
- 玻璃拟态 UI 设计

## 快速开始

### 安装依赖

```bash
npm install
```

### 开发模式

```bash
npm run dev
```

### 构建

```bash
npm run build
```

### 预览

```bash
npm run preview
```

## 使用示例

1. **输入目标单元总数**（如 8 个）
2. **点击「生成检测方案」**
3. **设置检测器状态**（根据实际检测结果切换开关）
4. **点击「定位异常」**
5. **查看结果**：系统自动计算并定位异常单元

## 技术栈

- **Vue 3** - 渐进式 JavaScript 框架
- **Vite** - 下一代前端构建工具
- **Element Plus** - Vue 3 组件库
- **@element-plus/icons-vue** - Element Plus 图标库

## 项目结构

```
poison-detector/
├── src/
│   ├── App.vue           # 主应用组件
│   ├── main.js           # 入口文件
│   ├── components/
│   │   ├── PlanTable.vue     # 检测方案表格
│   │   └── ResultPanel.vue   # 结果展示面板
│   └── utils/
│       └── detector.js   # 核心算法工具
├── index.html
├── package.json
└── vite.config.js
```

## 核心算法

```javascript
// 计算检测器数量
function calcProbeCount(n) {
  if (n <= 1) return 0
  return Math.ceil(Math.log2(n))
}

// 生成检测方案
function generatePlan(total) {
  const probeCount = calcProbeCount(total)
  // 每个检测器负责对应二进制位为 1 的单元
  ...
}

// 根据触发结果定位异常
function findPoisonBottle(deathResults, total) {
  // 将触发结果转换为二进制数
  // 触发=1, 未触发=0
  ...
}
```

## 在线演示

部署后即可访问。

## License

MIT
