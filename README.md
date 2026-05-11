# wechat-multi-open

一个面向 macOS 的微信多开脚本。它通过复制 `/Applications/WeChat.app`、修改副本的 Bundle ID，并重新签名副本来实现多实例启动。

## 功能

- 增量创建微信副本，最多支持 `20` 个总实例（含原版）
- 选择启动原版或指定副本，也支持一次启动全部
- 删除指定副本或恢复单开模式
- 为副本替换自定义图标，并在替换后重新签名

## 前置条件

- macOS
- 已安装原版微信：`/Applications/WeChat.app`
- 运行时可使用 `sudo`

脚本会依赖以下系统工具：

- `/usr/libexec/PlistBuddy`
- `codesign`
- `osascript`

## 使用方法

```bash
chmod +x wechat-multi-open.sh
./wechat-multi-open.sh
```

启动后会进入交互菜单：

1. 查看当前状态
2. 设置微信实例数量（含原版，范围 `2-20`）
3. 删除指定副本
4. 删除所有副本（恢复单开）
5. 选择启动微信实例
6. 停止所有微信进程
7. 自定义副本图标
8. 退出

## 图标与资源

- 图标资源位于 `icon/*.icns`
- 示例截图位于 `screenshots/`

图标替换只会修改选中的副本，不会删除原版微信。若 Dock 图标没有立即刷新，等待几秒或手动重启 Finder 即可。

## 注意事项

- 副本会创建在 `/Applications/WeChat2.app`、`/Applications/WeChat3.app` 等路径下
- 删除数据目录时，只会清理匹配的 `~/Library/Containers/com.tencent.xinWeChat*`
- 这是终端脚本，不是独立的图形界面应用
