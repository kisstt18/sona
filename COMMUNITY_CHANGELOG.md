# Sona 社区增强版

> 基于 [WJZ-P/sona](https://github.com/WJZ-P/sona) 的社区修改版本，修复了若干 bug 并新增了一些实用功能。

---

## 与原版的区别

### Bug 修复

| Issue | 修复内容 |
|-------|---------|
| 换楼后数据不刷新 | 队友交换楼层后，聊天框的 KDA/胜率数据自动重新发送，正确对应新楼层 |
| 聊天消息过于密集 | 新增分隔线和阶段标记（预选/锁定/换楼），方便区分每次数据发送 |
| 窗口尺寸异常 (#2, #15) | Wegame 对局助手窗口异常放大 + 客户端最小化恢复时尺寸异常，现已修复 |

### 新增功能

| 功能 | 说明 |
|------|------|
| 点击 PLAY 自动目标对局 (#20) | 开启后可设定目标队列，点击首页 PLAY 自动切换到指定模式 |
| 窗口异常修复 | 自动检测并修复客户端窗口尺寸异常 |

---

## 项目结构变化

新增的文件：

```
src/lib/features/
├── fix-lcu-window.ts       # 窗口异常修复
└── auto-target-queue.ts    # PLAY 自动目标队列
```

修改的文件：

```
src/lib/
├── features.ts              # 换楼检测、分隔线+阶段标记、新功能注册
└── store.ts                 # 新配置项注册
src/components/pages/
└── ToolsPage.tsx            # 新功能 UI 开关
src/lib/features/
└── global-particle.ts       # 粒子特效 canvas 尺寸限制
```

---

## 功能详情

### 换楼后数据自动刷新

队友在英雄选择阶段交换楼层后，`analyzeTeamPower` 会自动检测 `trades` 变化并重新发送队友战绩分析消息，确保楼层与数据对应正确。

### 消息分隔线与阶段标记

每条队友战绩分析消息顶部增加分隔线（`━━━`）和阶段标记：
- **预选英雄阶段** — 进入选人时
- **禁用/选择阶段** — 禁用/选择英雄时
- **锁定英雄阶段** — 锁定英雄时
- **英雄换楼阶段** — 队友交换楼层时

### 窗口异常修复

修复两个窗口尺寸问题：
1. 粒子特效 canvas 尺寸过大撑大 CEF 子窗口（Wegame 对局助手）
2. 客户端最小化恢复后 CEF 视口尺寸异常

### 点击 PLAY 自动目标对局

在 Sona 工具页 → 对局相关 中开启后，选择目标队列（匹配/排位/大乱斗/云顶），之后点击首页 PLAY 按钮会自动切换到指定模式。

---

## 安装

从本仓库的 Release 下载 `sona_community.zip`，解压后将 `sona` 文件夹放入 Pengu Loader 的 `plugins/` 目录，替换原版即可。

或手动构建：

```bash
npm install
npm run build
# 构建产物在 dist/ 目录，复制到 Pengu Loader plugins/sona/
```

---

## License

AGPL-3.0，与原项目保持一致。

---

基于 [WJZ-P/sona](https://github.com/WJZ-P/sona) 修改，感谢原作者的开源贡献。
