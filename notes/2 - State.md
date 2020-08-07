---
tags: [Notebooks/Coding Technology/Reactjs]
title: 2 - State
created: '2020-06-22T13:25:55.644Z'
modified: '2020-07-27T13:09:43.754Z'
---

# 2 - State
- State lưu trữ trạng thái của component
<details close>
<summary>Using State</summary>
<markdown>
- define
```js
import React from "react";

class App2 extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      date: new Date(),
    };
  }
  componentDidMount() {
    this.timeID = setInterval(() => this.tick(), 1000);
  }
  componentWillUnmount() {
    clearInterval(this.timeID);
  }
  tick() {
    this.setState({
      date: new Date(),
    });
  }
  render() {
    console.log(this);
    return (
      <div className="Application2">
        <div className="Header">ReactJS State 2</div>
        <div>{this.state.date.toLocaleTimeString()}</div>
      </div>
    );
  }
}

export default App2;

```
- using
```js
// chỉ cần gọi thôi. không cần làm gì hết
<App2></App2>

```
</markdown>
</details>

<details>
<summary>Right way using State</summary>
<markdown>
1. Do Not Modify State Directly
```js
// Wrong. Gọi trực tiếp thế này thì component không hiểu được cần phải re-render
// app sẽ ko render đúng ý ta
// nơi duy nhất có thể gán trực tiếp state là trong constructor
this.state.comment = 'Hello';

// Correct. Khi gọi hàm setState => component hiểu được cần re-render
this.setState({comment: 'Hello'});
```

2. State Updates May Be Asynchronous
```js
// Wrong. Vì tính chất Asynchronous, cả props lẫn state đều có thể bị call một lúc nhiều lần.
// Nếu ta cần sử dụng state và props để tính toán ra state mới thì không nên làm như sau.
this.setState({
  counter: this.state.counter + this.props.increment,
});

// Correct: update state theo props và state cũ. Dùng Arrow function
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));

// Correct: dùng function truyền thống
this.setState(function(state, props) {
  return {
    counter: state.counter + props.increment
  };
});
``` 

3. State Updates are Merged
```js
// khi ta gọi setState => nó sẽ merge object mới vào object cũ của ta. Nên không cần chỉ định tất cả state mà chỉ cần setState một phần là đủ
fetchPosts().then(response => {
  this.setState({
    posts: response.posts
  });
});

fetchComments().then(response => {
  this.setState({
    comments: response.comments
  });
});
```
</markdown>
</details>


