# 商务赋能平台

商务部内部使用的赋能平台，**单个 HTML 文件、零成本、无需服务器和数据库**。
所有数据保存在每个人自己浏览器的 localStorage 中，不上传任何服务器。

## 功能

**员工视角**
- 今日聚焦目标：打开页面的第一个交互，每天先锁定「今天最重要的一个数字」
- 📘 学习中心：4 门打法课程（有效沟通50人 / VIP社群转化 / 客户分层跟进 / 海外项目成交话术），可标记学习进度
- 🤖 AI训练室：6 个陪练场景（价格异议 / 已读不回 / 海外项目疑虑 / VIP入群被拒 / 话术润色 / 自由提问），输入「点评」可获得 AI 教练复盘
- 📝 日报录入：有效沟通 / 新增 / VIP意向 / 入群 / 成交 + 复盘与明日计划；一键复制日报文本发微信群；一键导出 JSON 发主管
- 📊 我的看板：今日/本周/本月统计、14天趋势图、目标进度条、连续打卡

**管理视角**
- 📥 数据汇总：批量导入成员导出的 JSON 文件（重复导入自动覆盖更新）
- 📈 团队看板：团队总量、今日日报提交率、7天团队趋势、成员排行榜（自动标记未报日报的人）

## 数据流转（无服务器方案）

1. 员工每天填日报 → 点「复制日报文本」→ 粘贴到微信群（本来就要发的日报）
2. 主管把群里的日报消息**整段复制**（可以连聊天一起复制，多人多天都行）
3. 切到「管理视角 → 数据汇总」→ 粘贴 → 点「解析并导入」→ 团队看板自动汇总

> 备用方式：员工也可点「导出我的数据」生成 JSON 文件发给主管导入。

## 使用方式（三选一，都免费）

### 1. 直接打开（最简单）
把 `index.html` 发给每位同事，双击用浏览器打开即可。

### 2. 局域网共享
在本文件夹运行：
```bash
python3 -m http.server 8000
```
同事在同一 WiFi 下访问 `http://你的电脑IP:8000`（查 IP：`ipconfig getifaddr en0`）。
注意：数据仍存在各自浏览器里，换浏览器/设备数据不互通。

### 3. GitHub Pages（推荐，有固定网址）
```bash
cd 商务赋能平台
git init && git add . && git commit -m "init"
gh repo create swfn-platform --private --source=. --push
gh api repos/{owner}/swfn-platform/pages -X POST -f build_type=workflow 2>/dev/null || true
```
或者最简单的方式：在 GitHub 新建仓库 → 上传 `index.html` → Settings → Pages → 选择 main 分支 → 获得 `https://用户名.github.io/仓库名/` 网址发给团队。

> 私有仓库的 Pages 需要付费版；用免费版请建**公开仓库**（页面本身不含任何公司数据，数据都在各自浏览器本地，安全无虞）。

## AI训练室接口配置

- 在「AI训练室 → 接口设置」填入 API 地址、模型、Key，支持一切 **OpenAI 兼容**接口：
  - DeepSeek：`https://api.deepseek.com` / `deepseek-chat`（费用极低）
  - Kimi：`https://api.moonshot.cn/v1` / `moonshot-v1-8k`
  - 通义：`https://dashscope.aliyuncs.com/compatible-mode/v1` / `qwen-plus`
- Key 只保存在本机浏览器，不会上传
- **没有 Key 也能用**：点「复制完整提示词」，粘贴到豆包/Kimi/DeepSeek 网页版即可继续对练

## 自定义内容

打开 `index.html` 搜索 `COURSES`（课程内容）和 `SCENARIOS`（AI陪练场景），按现有格式增删修改即可，无需任何编程基础以外的工具。
