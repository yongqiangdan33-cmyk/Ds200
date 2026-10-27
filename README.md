# 我们的小日子

温暖手账风格的双人空间，包含照片墙、在一起天数、重要日子倒计时、心愿、可点按移动的 3D 回忆展馆、回收站、备份及离线纪念册。

## 当前进度

GitHub Pages 当前运行本地演示模式：记录保存在各自浏览器，尚不互通。云端登录、两人成员绑定、私有照片接口、版本冲突处理及清理任务的代码已经加入，但尚未部署到真实云环境，不能将本地测试当作线上权限验收。

正式接入步骤见 [CloudBase 部署指南](https://github.com/yongqiangdan33-cmyk/Ds200/blob/main/云端接通指南.md)。前端可以继续使用现有 GitHub Pages 地址，无需另购前端域名。账号注册、实名认证、套餐选择和支付由用户自行完成。私人照片不要上传到公开 GitHub 仓库。

## 本地运行

```sh
pnpm install --frozen-lockfile
pnpm dev
```

默认 `VITE_APP_MODE=demo`。在空间设置填写称呼和开始日期，通过页面新增内容。展馆拖动转头，点击地面圆环移动，点击展品看故事；不支持 WebGL 时使用藏品列表。

```sh
pnpm test
pnpm typecheck
pnpm build
pnpm build:single
pnpm build:cloud
```

`build:single` 生成独立 HTML，`build:cloud` 生成两个云函数目录。云端网页必须配置 `.env.local` 后使用 `pnpm build:cloud-web`，参见部署指南。禁止在 VITE 变量中放入密码或管理员密钥。

## 数据说明

- 演示数据保存在当前浏览器 IndexedDB；清除浏览器数据可能丢失，请保存原片并导出备份。不同地址、设备和浏览器之间不自动迁移。
- 图片会转为压缩 JPG 展示版本，去除原始元数据。HEIC 支持取决于浏览器，不支持时先转 JPG/PNG。
- 本地演示超过 30 天的回收记录在页面打开时清理；云端清理由后台定时函数执行。
- 离线纪念册 ZIP 解压后打开 index.html。备份暂不支持自动恢复导入。云端导出上限 100 MB，尚无分批选择界面。
- 云端使用 5 分钟临时图片链接，持有链接的人在有效期内可访问。真实环境的鉴权、跨域、链接过期及两台手机网络验收尚未执行。
- 心愿关联回忆、展馆按年筛选和完整真实手机验收仍待完成。

## 发布

当前 Ds200 仓库使用 main 分支根目录的独立 index.html，由 GitHub Pages 发布。源码项目中的开发 index.html 不能直接替代它。源码内另附 GitHub Actions 工作流，只有采用展开的源码仓库并改用 Actions 发布时才使用。
