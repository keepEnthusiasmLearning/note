# Web Storage API

提供访问**特定域名**下的 sessionStorage 会话储存或 localStorage 本地储存功能。

- Storage.length: Number - 储存的数据量 
- Storage.key(n) - 返回储存的第 n 个健名
- Storage.getItem(key: string) - 返回指定健值
- Storage.setItem(key, val) - 设置或添加指定健值
- Storage.removeItem(key) - 删除指定健
- Storage.clear() - 清空所有健

## Window.localStorage

本地缓存，数据将长期保存在用户本地设备。

## Window.sessionStorage

会话储存，数据将在会话结束后清楚。