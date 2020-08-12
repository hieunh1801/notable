---
tags: [Notebooks/Coding Technology/Reactjs]
title: Redux - Part 1
created: '2020-08-12T01:18:44.725Z'
modified: '2020-08-12T02:02:13.318Z'
---

# Redux - Part 1
https://redux.js.org/introduction/getting-started

### Principle 
- Reducer không làm thay đổi trực tiếp state. thay vào đó trả về một state mới
- Dữ liệu được lưu ở một nguồn duy nhất là store
- Dữ liệu chỉ được cập nhật khi gọi tới dispatch

### Khái niệm
- Redux là gì?
  - Là một thư viện giúp reactjs quản lý state
- __Store__: là nơi lưu trữ state của cả ứng dụng
- __Action__: mang thông tin update state
- __Reducer__: nhận input là action và preState => trả về newState

### Scenarior
<details close>
<summary>Basic Scenarior</summary>

1. Tạo Store
2. Lấy dữ liệu từ Store
3. Cập nhật Store

```js
import React from "react";
import { createStore } from "redux";
// Khai bao action
const INCREMENT = "INCREMENT";
const DECREMENT = "DECREMENT";

const actionIncrement = (amount) => {
  return {
    type: INCREMENT,
    payload: { amount },
  };
};

const actionDecrement = (amount) => {
  return {
    type: DECREMENT,
    payload: { amount },
  };
};

// INITIAL STATE
const initialState = 0;

const reducerCounter = (preState = initialState, action) => {
  switch (action.type) {
    case INCREMENT:
      const { amount: incrementAmount = 0 } = action.payload;
      console.log("reducerCounter - INCREMENT");
      return preState + incrementAmount;
    case DECREMENT:
      console.log("reducerCounter - DECREMENT");
      const { amount: decrementAmount = 0 } = action.payload;
      return preState - decrementAmount;
    default:
      console.log("reducerCounter - default");
      return preState;
  }
};

// 1. Khoi tao store
const store = createStore(reducerCounter);

// 2. Lay ra state
let state = store.getState();
console.log("Create store success state=", state);

// 3. Cap nhat store
store.dispatch(actionIncrement(5));
state = store.getState();
console.log("Increment 5 unit state=", state);

store.dispatch(actionDecrement(2));
state = store.getState();
console.log("actionDecrement 2 unit state=", state);

// Xem gia tri state sau khi cap nhat
const App1ReduxBasic = () => {
  return <h1>Redux Basic</h1>;
};

export default App1ReduxBasic;

```
</details>
