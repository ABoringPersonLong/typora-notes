# 快捷键：

Ctrl + PgUp：上一个编辑器

Ctrl + PgDn：下一个编辑器

Ctrl + Shift + [：折叠光标所在的区域

Ctrl + Shift + ]：打开光标所在的区域

Ctrl + k + 0：折叠所有区域代码

Ctrl + K + J：展开所有区域代码

Alt + 上下键：移动当前这一行的代码

Ctrl + 上下键：移动滚动条

Ctrl + /：注释

Ctrl + J：打开/关闭终端

Ctrl + Shift + `：新建一个终端

Shift + Alt + 上下键：复制当前行到下一行

Ctrl + Shift + K：删除当前行

Ctrl + P：全局查找文件

Shift + Alt + F：代码格式化

Ctrl + Shift + N：打开一个新窗口

Ctrl + F：当前文件搜索

Ctrl + Shift + F：全局搜索

Ctrl + H：当前文件替换

Ctrl + Shift + H：全局替换

Ctrl + R：打开最近打开的文件

Ctrl + Shift + C：打开新的命令窗

Ctrl + 1/2/3：分屏

# 设置：

## 1.底部状态栏颜色：

Settings -> Workspace -> Workbench -> Appearance -> Edit in settings.json

将内容改成：

```json
{
    "workbench.activityBar.visible": true,
    "workbench.colorCustomizations": {
        "statusBar.background": "#323234"
    }
}
```

## 2.代码提示快捷键：

File -> Preferences -> Keyboard Shortcuts

搜索 ctrl+space，找到 Trigger Suggest，修改成 alt+/

## 3.设置格式化时 tab 缩进为 4 个空格

1. 在设置中搜索 tab
2. 将 **Editor: Tab Size** 打勾
3. 再点击 **Editor: Detect Indentation** 跳转过去将勾取消掉