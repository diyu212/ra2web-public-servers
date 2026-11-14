# RA2WEB 公开联机服务器列表（SF南京区 备用服）

把下面列表加进你的 **ra2web / 网页红警 / 红色井界** 客户端，即可连入本站服务器联机对战。

> 本列表由「SF南京区(备用服务器)」运营方维护，公开免费、非商业用途。
> 使用本列表即表示你同意遵守 RA2WEB / 网页红井 / 红色井界 的许可条款（仅个人研究/爱好，禁止商用）。

---

## 一、服务器清单（2026-11-14 生效）

| 标识 | 名称 | 说明 | WOL 接入点 |
|------|------|------|------------|
| `CHN1` | 外网测试服（华北大区） | 主服，经本站反代到上游华北节点 | `wss://ab410af2bd47bf649.app.workbuddy.host/wol` |
| `SELF1` | SF南京区(备用服务器) | 本站自建 selfwol 中继（备用） | `wss://ab410af2bd47bf649.app.workbuddy.host/self/wol` |

两服均**公网可达**，账号互通（同一套 register/login），地图/资源经本站中转。

---

## 二、怎么加进你的客户端

### 方式 A：ra2web 一键部署（GitHub Pages / EdgeOne / Vercel fork 版）
1. 打开你 fork 的仓库里的 `servers.ini`。
2. 把本仓库 `servers.ini` 的内容**整段替换**进去。
3. 提交并重新部署，浏览器**强制刷新（Ctrl+F5）**重新拉取列表。

### 方式 B：直接改本地站点
把你站点的 `servers.ini` / `servers-v3.ini` 换成[本仓库同名文件](./servers.ini)，重启前端即可。

### 方式 C：浏览器控制台临时注入（仅当前会话有效，不落盘）
```js
// 在 ra2web 页面按 F12 打开控制台粘贴执行，刷新大厅生效（下次打开需重跑）
localStorage.setItem('extraServers', JSON.stringify([
  { id:'CHN1', label:'外网测试服（华北大区）', wolUrl:'wss://ab410af2bd47bf649.app.workbuddy.host/wol', apiBase:'https://ab410af2bd47bf649.app.workbuddy.host' },
  { id:'SELF1', label:'SF南京区(备用服务器)', wolUrl:'wss://ab410af2bd47bf649.app.workbuddy.host/self/wol', apiBase:'https://ab410af2bd47bf649.app.workbuddy.host/self' }
]));
```
> 注：是否读取 `extraServers` 取决于你的客户端版本，方式 A/B 最稳妥。

---

## 三、客户端格式（ra2web v0.78.x）

```
[CHN1]
label="外网测试服（华北大区）"
available=yes
gameVersion=0.78
wolUrl="wss://ab410af2bd47bf649.app.workbuddy.host/wol"
apiRegUrl="https://ab410af2bd47bf649.app.workbuddy.host/register"
wladderUrl="https://ab410af2bd47bf649.app.workbuddy.host/ladder"
wgameresUrl="https://ab410af2bd47bf649.app.workbuddy.host/wgameres"
mapTransferUrl="https://ab410af2bd47bf649.app.workbuddy.host/map-transfer"

[SELF1]
label="SF南京区(备用服务器)"
available=yes
gameVersion=0.78
wolUrl="wss://ab410af2bd47bf649.app.workbuddy.host/self/wol"
apiRegUrl="https://ab410af2bd47bf649.app.workbuddy.host/self/register"
wladderUrl="https://ab410af2bd47bf649.app.workbuddy.host/self/ladder"
wgameresUrl="https://ab410af2bd47bf649.app.workbuddy.host/self/wgameres"
mapTransferUrl="https://ab410af2bd47bf649.app.workbuddy.host/self/map-transfer"
```

- `wolUrl`：大厅/账号 WebSocket（WOL 协议）
- `apiRegUrl` / `wladderUrl` / `wgameresUrl` / `mapTransferUrl`：注册、天梯、资源、地图中转的 HTTP/HTTPS 接口
- `gameVersion=0.78`：客户端版本号，低于此版本的客户端可能无法进入（请保持客户端为 v0.78.x）

---

## 四、重要说明 / 免责

1. **沙箱主机名可能变更**：当前公网地址 `ab410af2bd47bf649.app.workbuddy.host` 是临时沙箱域名。若服务迁移到固定域名，请替换上面所有 `ab410af2bd47bf649.app.workbuddy.host` 为新域名后重新发布。
2. **版本匹配**：请使用与本列表 `gameVersion` 一致的客户端，跨大版本可能无法联机。
3. **资源自动加载**：进实际对局前客户端会自动从本站拉取完整资源包，请勿手动导入冲突包。
4. **仅限非商业、个人研究/爱好用途**，遵守 RA2WEB / 网页红井 / 红色井界 许可。

---

## 五、自助排查

- 连不上：先 `Ctrl+F5` 强刷；再看浏览器 F12 控制台是否有 WS 连接报错。
- 进房后加载崩溃：确认客户端版本与 `gameVersion` 一致，且资源包已自动加载完成。
- 仍不行：把 F12 控制台报错发运营方即可定位。
