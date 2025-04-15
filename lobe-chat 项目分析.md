# lobe-chat 项目分析

## 主界面结构



## 左侧 Session

使用了 react 异步组件 `Suspense` 和 `lazy()`，具体没细看，有空再了解

## 聊天框

### Desktop

由 DesktopChatInput 组成，传递参数为

```tsx
inputHeight													// 输入框高度
onInputHeightChange									// 监听高度变化
leftActions													// header 左侧结构
rightActions												// header 右侧结构
renderFooter={renderFooter}					// footer 渲染函数
renderTextArea={renderTextArea}			// textArea 输入框渲染函数
```

### DesktopChatInput

由可拖拽面板 `<DraggablePanel>` 包裹，来源于 `@lobehub/ui`，其中的高度配置来自于全局变量 `@/const/layoutTokens`

## api 配置



## 对话页面

使用 `react-virtuoso` 作超长对话列表的高性能渲染。只渲染可视区的 dom。

## 语音对话

