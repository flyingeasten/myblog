---
title: "MsgBox函数消息框图标类型"
date: 2025-08-31T11:06:05.367Z
draft: false
tags: []
---

---
Project: ["VBA学习"]
---
VBA 中 `MsgBox` 函数用于指定消息框图标类型的常量如下，
它们用于向用户传达不同类型的信息或提示。以下是对这些常量的简单总结：

### 1. **`vbCritical`**
- **图标**：红色叉号（表示错误或严重问题）。
- **用途**：用于显示错误信息或严重问题。
- **示例**：
  ```vba
  MsgBox "发生严重错误，请联系管理员！", vbCritical
  ```

### 2. **`vbInformation`**
- **图标**：蓝色“i”（表示信息性消息）。
- **用途**：用于显示普通信息或提示。
- **示例**：
  ```vba
  MsgBox "操作成功完成！", vbInformation
  ```

### 3. **`vbExclamation`**
- **图标**：黄色感叹号（表示警告或需要注意的信息）。
- **用途**：用于显示警告信息或需要注意的内容。
- **示例**：
  ```vba
  MsgBox "您即将删除重要数据，是否继续？", vbExclamation + vbYesNo
  ```

### 4. **`vbQuestion`**
- **图标**：蓝色问号（表示询问用户）。
- **用途**：用于询问用户是否要执行某个操作。
- **示例**：
  ```vba
  MsgBox "您确定要退出程序吗？", vbQuestion + vbYesNo
  ```

### 总结
这些常量用于在 `MsgBox` 函数中指定消息框的图标类型，帮助用户更好地理解消息的性质：

- **`vbCritical`**：红色叉号，表示错误或严重问题。
- **`vbInformation`**：蓝色“i”，表示普通信息或提示。
- **`vbExclamation`**：黄色感叹号，表示警告或需要注意的内容。
- **`vbQuestion`**：蓝色问号，表示询问用户。

### 示例代码
```vba
' 显示错误消息
MsgBox "发生严重错误，请联系管理员！", vbCritical

' 显示信息消息
MsgBox "操作成功完成！", vbInformation

' 显示警告消息
MsgBox "您即将删除重要数据，是否继续？", vbExclamation + vbYesNo

' 显示询问消息
MsgBox "您确定要退出程序吗？", vbQuestion + vbYesNo
```