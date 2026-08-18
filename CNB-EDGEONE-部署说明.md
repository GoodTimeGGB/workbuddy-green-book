# WorkBuddy 绿皮书 · CNB + EdgeOne 部署清单

目标：把绿皮书（静态站点）托管到 **CNB（cnb.cool）** 作为代码源与 CI，
前面套 **EdgeOne** 做免费全球加速 —— 国内直连、零流量分发费。

---

## 架构（你要的方案）

```
读者浏览器
   │  http://workbuddy.wangjin.site/
   ▼
腾讯云 DNSPod（CNAME: workbuddy → EdgeOne 加速域名）   ← 你已加过，改指向即可
   ▼
EdgeOne（免费版：国内节点 + 全球加速 + 自动 HTTPS + DDoS/WAF）  ← 加速层
   ▼
CNB 仓库（cnb.cool）+ EdgeOne Pages（托管绿皮书静态文件）        ← 源站
```

两种方式任选其一：

### 方式 A（推荐，最省事）：CNB 流水线 → EdgeOne Pages
代码进 CNB，CNB 的 `.cnb.yml` 流水线一键 `npx edgeone pages deploy` 把站点推到
EdgeOne 网络。托管+加速都在 EdgeOne 上，免费、国内快。
- 本目录已备好 `.cnb.yml`（指向 EdgeOne Pages 项目 `workbuddy-green-book`）。

### 方式 B（最贴合原话：CNB 托管 + EdgeOne 仅加速）
CNB Pages 作为源站，EdgeOne 仅做 CDN 加速（CNAME 接入）。
- CNB 仓库开 Pages（控制台一键），拿到 `*.pages.cnb.run` 源站域名；
- EdgeOne 加站点 `workbuddy.wangjin.site`，源站填 CNB Pages 域名，CNAME 接入；
- DNS：`workbuddy` CNAME → EdgeOne 分配的加速域名。

---

## 操作步骤（方式 A）

1. **建 CNB 仓库**
   - 登录 cnb.cool，新建仓库（如 `workbuddy-green-book`），把本 `deploy/` 目录内容
     （index.html + assets/ + .cnb.yml）推上去。
   - 或用「从 GitHub 导入」直接导入 `github.com/GoodTimeGGB/workbuddy-green-book`。

2. **建 EdgeOne Pages 项目**
   - 腾讯云 EdgeOne 控制台 → Pages → 新建项目 `workbuddy-green-book`（类型：直接上传）。
   - 记下项目名（与 `.cnb.yml` 里的 `-n` 一致）。

3. **配 EDGEONE_API_TOKEN**
   - EdgeOne Pages 控制台生成 API Token；
   - 在 CNB 仓库「变量/密钥」里新增 `EDGEONE_API_TOKEN`，值填该 Token。

4. **绑定自定义域名**
   - EdgeOne Pages 项目里添加自定义域名 `workbuddy.wangjin.site`，按提示验证；
   - 拿到 EdgeOne 分配的 CNAME（如 `workbuddy.wangjin.site.eo.dnse*.com`）。

5. **改 DNS（关键）**
   - 去腾讯云 DNSPod，把 `workbuddy` 的 CNAME 值从 `goodtimeggb.github.io`
     **改成第 4 步 EdgeOne 给的加速域名**。
   - 等 5–30 分钟传播，访问 `http://workbuddy.wangjin.site/` 即上线。
   - 生效后 EdgeOne 自动签发 HTTPS，控制台勾选 Enforce HTTPS。

6. **自动部署**
   - 以后绿皮书升版：更新 `index.html` + `assets/` → `git push` 到 CNB main →
     流水线自动重新部署到 EdgeOne Pages，无需手动操作。

---

## 本地已完成的准备
- [x] `deploy/index.html` 正文 49 张配图已补齐（之前缺失会裂图，已修）
- [x] 封面 IP 形象 1.8MB→103KB、Logo 923KB→24KB（规避 EdgeOne 免费版大图限流）
- [x] `.cnb.yml` 流水线配置（方式 A）
- [x] 系统字体栈（零外部依赖，国内秒开）

## 待你操作
- [ ] 连接 WorkBuddy 里的 **CNB** 与 **EdgeOne / EdgeOne Pages** 连接器（或网页端手动完成上面 1–5 步）
- [ ] 改 DNS 指向 EdgeOne
- [ ] 旧的 workbuddy.link 页面（误建的）建议取消发布，避免读者分流
