# 部署到 GitHub Pages

这个目录是 `Pr0b1em/Pr0b1em.github.io` 的克隆，内容已经替换成修好备案的新构建。只差一步推送。

## 方式一：用 Token 推（最快）

去 GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens 生成一个，权限选 `Pr0b1em/Pr0b1em.github.io` 仓库的 **Contents: Read and write**。

然后在本目录执行：

```bash
git add -A
git commit -m "fix: 修正备案号为 渝ICP备2024047956号-1 并指向 beian.miit.gov.cn"
git push origin main
```

推送时用户名填 GitHub 用户名，密码填刚生成的 token。

或者直接把 token 塞进地址里（注意别泄露）：

```bash
git push https://<用户名>:<token>@github.com/Pr0b1em/Pr0b1em.github.io.git main
```

## 方式二：在 GitHub 网页上

先在本目录打包：

```bash
git add -A
git commit -m "fix: 修正备案号"
git bundle create site.bundle main
```

不推荐，621 个文件手传太慢，用方式一。

## 方式三：本地重新构建再推

如果不想用这份现成的，可以在 `hexo-project` 里自己构建：

```bash
cd hexo-project
npx hexo clean && npx hexo generate
cd public
git init && git remote add origin https://github.com/Pr0b1em/Pr0b1em.github.io.git
git add -A && git commit -m "update"
git push -f origin main
```

## 推完确认

1. 等 1-2 分钟，打开 http://pr0b1em.top/
2. 拉到页脚，应该看到 `渝ICP备2024047956号-1`，点击跳到 `beian.miit.gov.cn`
3. 确认后去阿里云备案控制台重新提交审核

截止时间 **2026-10-22 16:00**。

## 这次改了什么

页脚从：

```html
<a href="https://www.beian.gov.cn" target="_blank">渝ICP备2024047956号 | 渝公网安备50011702501074号</a>
```

（备案号缺 `-1`，且两个备案号挤在同一个指向公安备案站的链接里）

改成：

```html
<a href="https://beian.miit.gov.cn/" target="_blank">渝ICP备2024047956号-1</a>
 | <a href="https://www.beian.gov.cn" target="_blank">渝公网安备50011702501074号</a>
```

第二个链接是原来就有的公安备案，保留不动。
