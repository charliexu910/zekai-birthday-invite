# 许泽恺 · LEVEL 10 生日闯关派对邀请函

《我的世界》像素风手机 H5 邀请函，含 RSVP 回执（参加/不参加 + 大人小孩人数），
回复可自动记录到云端名单。

## 一、记录参加/不参加名单（2 分钟配置）

页面默认只在宾客手机本地保存回复。填一个表单地址，即可让**每份回执（参加和不参加）自动汇总到你的后台**：

1. 打开 [formspree.io](https://formspree.io)（免费，国内可直连），注册/登录
2. 点 **New form**，名字随便填（如 `zekai-birthday`），创建后复制形如
   `https://formspree.io/f/abcdwxyz` 的地址
3. 用编辑器打开 `index.html`，找到这一行（搜索 `RSVP_ENDPOINT`）：

   ```js
   var RSVP_ENDPOINT = ""; // ★ 把你的地址填进引号里
   ```

   改成：

   ```js
   var RSVP_ENDPOINT = "https://formspree.io/f/abcdwxyz";
   ```

4. 保存、重新部署。完成 ✅

之后每位宾客点「发送回执」，名单里就会多一行：**回复（参加/不参加）、称呼、大人、小朋友、合计、留言、提交时间**，每条还会发邮件提醒你。在 Formspree 后台 **Submissions** 页可查看全部记录并导出 CSV（Excel）。

> 微信内打开若同步失败，页面会自动提示宾客用「复制回执」发微信，双保险。

## 二、部署到你的 page

整个文件夹（`index.html` + `images/`）就是纯静态网站，放到任何静态托管即可。

### 方式 A：GitHub Pages

```bash
cd birthday-invite
git remote add origin git@github.com:<你的用户名>/<仓库名>.git
git push -u origin main
```

然后 GitHub 仓库 → **Settings → Pages** → Source 选 `main` 分支 `/ (root)` → Save。
约 1 分钟后访问 `https://<你的用户名>.github.io/<仓库名>/`。

> 提示：github.io 在大陆访问时快时慢。如果宾客主要在大陆，建议方式 B 或 C。

### 方式 B：腾讯云 COS 静态网站（大陆访问最稳）

1. 腾讯云控制台 → 对象存储 → 创建存储桶（地域选上海，权限：公有读私有写）
2. 上传本文件夹全部内容（保持 `images/` 目录结构）
3. 存储桶 → 基础配置 → 静态网站 → 开启，索引文档填 `index.html`
4. 用分配的默认域名访问（默认域名无需备案）

### 方式 C：已有服务器 / 宝塔 / nginx

把文件夹上传到网站目录（如 `/www/wwwroot/invite/`），直接访问即可。

## 三、改内容

所有文字都在 `index.html` 里，搜索中文直接改；照片在 `images/`，同名替换即可。

## 本地预览

```bash
cd birthday-invite && python3 -m http.server 8765
# 浏览器打开 http://127.0.0.1:8765
```
