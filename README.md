# Mochi Web App（PWA）

把 `Mochi-交互原型.html` 打包成的可安装 Web 应用。部署到任意 HTTPS 静态托管后，手机浏览器打开 →「添加到主屏幕」，即可像原生 App 一样全屏运行、离线打开。

## 目录内容

| 文件 | 作用 |
|---|---|
| `index.html` | 原型页（与主原型同步 + PWA 标签和 Service Worker 注册） |
| `manifest.webmanifest` | 应用名、图标、竖屏独立窗口等安装信息 |
| `sw.js` | Service Worker：缓存页面和图标，离线可打开；网络优先策略，更新后刷新一次拿新版 |
| `icons/` | 192/512/180/32 PNG 图标 + maskable 版 + SVG 源文件 |

## 部署方式（三选一）

**GitHub Pages（免费）**
```bash
cd mochi-webapp
git init && git add -A && git commit -m "Mochi webapp"
gh repo create mochi-prototype --public --source=. --push
# Settings → Pages → 选 main 分支，几分钟后访问
# https://<你的用户名>.github.io/mochi-prototype/
```

**Netlify / Vercel（免费，最快）**
把 `mochi-webapp` 文件夹拖进 https://app.netlify.com/drop 即可，10 秒拿到 HTTPS 地址。

**自己手机上快速体验（不需要公网）**
```bash
cd mochi-webapp && python3 -m http.server 8000
# 手机和电脑连同一 Wi-Fi，访问 http://<电脑局域网IP>:8000
# 注意：iOS Safari 添加到主屏幕后离线功能受限（非 HTTPS 时 SW 不生效）
```

## 安装到主屏幕

- **iOS Safari**：分享按钮 → 添加到主屏幕
- **Android Chrome**：地址栏右侧安装提示，或菜单 →「安装应用」

## 更新原型内容

主原型 `Mochi-交互原型.html` 改完后，在项目根目录重新生成：
```bash
python3 - <<'EOF'
src = open('Mochi-交互原型.html', encoding='utf-8').read()
# （同 build 脚本：注入 PWA 头 + SW 注册）
EOF
```
或者直接告诉我"同步 webapp"，我来重新打包并升 SW 缓存版本号。
