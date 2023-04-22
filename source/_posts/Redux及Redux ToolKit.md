title: redux及Redux ToolKit
author: 黄罐头
tags: ['redux','react']
categories: web

date: 2023-01-08 17:28:00
---

## Redux是什么

**Redux 是一个使用叫做 “action” 的事件来管理和更新应用状态的模式和工具库** 它以集中式 **Store** 的方式对整个应用中使用的状态进行集中管理，确保状态只能以可预测的方式更新。



## Redux ToolKit是什么

**Redux Toolkit** 是官方推荐的编写 **Redux** 逻辑的方法。 它包含我们对于构建 **Redux** 应用程序必不可少的包和函数。 **Redux Toolkit** 的构建简化了大多数 **Redux** 任务，防止了常见错误，并使编写 **Redux** 应用程序变得更加容易。可以说 **Redux Toolkit** 就是目前 **Redux** 的最佳实践方式。



## 如何实现RTK

```typescript
// counterSlice.ts 文件

import { createSlice } from '@reduxjs/toolkit';

export interface CounterState {
  value: number;
  title: string
}
const initialState: CounterState = {
  value: 0,
  title: "redux toolkit pre"
};

// 创建一个 Slice 
export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  // 定义 reducers 并生成关联的操作
  reducers: {
    // 定义一个加的方法
    increment: (state) => {
      state.value += 1;
    },
    // 定义一个减的方法
    decrement: (state) => {
      state.value -= 1;
    },
  },
});
// 导出加减的方法
export const { increment, decrement } = counterSlice.actions;

// 默认导出
export default counterSlice.reducer;
```

```typescript
// index.ts 文件

import { configureStore } from "@reduxjs/toolkit";
import counterSlice from "./features/counterSlice.ts";

// configureStore创建一个redux数据
const store = configureStore({
  // 合并多个Slice
  reducer: {
    counter: counterSlice
  },
});

export default store;
```

```jsx
//index.tsx文件

import ReactDOM from 'react-dom/client'
import App from './App'
import { Provider } from 'react-redux'
import store from './redux'

ReactDOM.createRoot(document.getElementById('root') as HTMLElement).render(
  <Provider store={store}>
    <App />
  </Provider>
)
```

```jsx
// App.tsx 文件

// 引入相关的hooks
import {useSelector, useDispatch} from 'react-redux';
// 引入对应的方法
import {increment, decrement} from './store/features/counterSlice.ts';
import './App.css';

function App() {
  // 通过useSelector直接拿到store中定义的value
  const { value } = useSelector((store)=>store.counter)
  // 通过useDispatch 派发事件
  const dispatch = useDispatch()
  return (
    <>
        {/* 页面中应用的代码 */}
        <p>{value}</p>
        <button onClick={()=>{dispatch(increment())}}>加</button>
        <button onClick={()=>{dispatch(decrement())}}>减</button>
    </>
  );
}

export default App;
```

