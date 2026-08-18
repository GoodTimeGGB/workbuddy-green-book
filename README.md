# WorkBuddy 绿皮书

**AI Agent 办公新物种 · 全景实战指南**

> v4.11 · 2026.08 · 135 章 · 40 大部分 · 约 890 页

## 这是什么

WorkBuddy 绿皮书是一份**单文件 HTML 电子书**，系统梳理腾讯 AI 智能体工作台 **WorkBuddy** 的产品能力、实战技巧、生态动态与行业落地案例。

以腾讯官方信源为主干（腾讯新闻、腾讯云开发者社区、腾讯研究院、官方公众号等），交叉印证权威媒体与一线实践者反馈，覆盖从零入门到企业级落地的完整路径。

## 快速访问

| 渠道 | 地址 |
|------|------|
| GitHub Pages | https://workbuddy.wangjin.site |
| EdgeOne 加速版 | （待 CNB 导入后绑定） |

> **提示**：国内访问建议走 EdgeOne 加速域名（见下方部署说明）。

## 内容概览

- **认识与入门** — 产品定位、安装配置、工作模式、模型选择
- **核心能力** — Skills 技能系统、连接器、自动化、专家团
- **场景实战** — 办公、PPT、代码开发、内容创作、深度研究
- **最佳实践** — 提示词工程、多智能体协作、记忆管理
- **行业落地** — 政务、制造、金融、教育等 50+ 行业案例
- **官方动态** — 2026 年 7–8 月最新进展（每日更新）
- **生态全景** — Agent 舰队战略、Q2 财报数据、OPC 社区、开发者沙龙
- **附录** — 技能清单、FAQ、快捷键、版本更新日志

## 部署说明

本项目支持两种部署方式：

### A. GitHub Pages（当前生效）

仓库已配置 CNAME → `workbuddy.wangjin.site`，GitHub Pages 自动构建。

### B. CNB + EdgeOne 全球加速（推荐）

1. 登录 [cnb.cool](https://cnb.cool) → 新建仓库 → **导入外部仓库**
2. 填入：`https://github.com/GoodTimeGGB/workbuddy-green-book`
3. 导入后 CNB 自动识别 `.cnb.yml` 流水线，一键部署至 EdgeOne Pages
4. 到 DNSPod 将 `workbuddy.wangjin.site` 的 CNAME 改为 EdgeOne 提供的加速域名

详细步骤见仓库内 [`CNB-EDGEONE-部署说明.md`](./CNB-EDGEONE-部署说明.md)

## 文件结构

```
├── index.html          # 主文件（单文件电子书，含全部章节 + 内联样式 + 二维码）
├── assets/             # 正文配图（50+ 张官方截图 / 现场照片）
│   ├── ip-character.jpg    # 个人 IP 形象
│   ├── logo.jpg            # 品牌 Logo
│   └── wb-*.png/jpg        # WorkBuddy 官方素材
├── .cnb.yml            # CNB EdgeOne 部署流水线配置
├── CNAME               # GitHub Pages 自定义域名
├── CNB-EDGEONE-部署说明.md
└── README.md           # 本文件
```

## 关于作者

**王总（GoodTime）** — 全栈开发者 · AI 科普创作者

- 微信公众号「宁的AI小站」
- GitHub: [@GoodTimeGGB](https://github.com/GoodTimeGGB)

## License

[MIT](LICENSE)
