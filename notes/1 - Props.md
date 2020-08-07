---
tags: [Notebooks/Coding Technology/Reactjs]
title: 1 - Props
created: '2020-06-22T13:25:49.237Z'
modified: '2020-07-27T13:09:49.040Z'
---

# 1 - Props
- Không bao giờ thay đổi props (giống pure function)
<details close>
<summary>Using Props</summary>
<markdown>
- define
```js
// CÁCH 1: FUNCTIONAL COMPONENT
function App1(props) {
  console.log(props);
  return (
    <div className="App1">
      <div className="Header">
        This is {props.title ? props.title : "Default Name"}
      </div>
    </div>
  );
}

// CÁCH 2: CLASS COMPONENT
class App1 extends React.Component {
  render() {
    return (
      <div className="App1">
        <div className="Header">
          This is {this.props.title ? this.props.title : "Default Name"}
        </div>
      </div>
    );
  }
}
```
- using
```js
// khi truyền thì tên props là title
<App1 title="Application 1"></App1>

// trường hợp missing props thì component vẫn chạy bình thường
// tuy nhiên nếu cần phải lấy props để tính toán thì lại là chuyện khác
```
</markdown>
</details>


