---
tags: [Notebooks/Coding Technology/Reactjs]
title: 6 Handling Form
created: '2020-06-23T01:18:02.077Z'
modified: '2020-06-23T01:47:07.099Z'
---

# 6 Handling Form
- form sử dụng state để lưu trạng thái => còn gọi là controll component
- để sử dụng các giá trị từ form và cập nhật trường thông tin ta sử dụng state của component
- Dùng thư viện nếu thấy thích https://github.com/jaredpalmer/formik
<details close>
<summary>Lưu ý: nếu không dùng arrow function mà viết function thuần</summary>
<markdown>
> Khi dùng class Component => để sử dụng con trỏ this(javascript thuần) trong các function thì phải bind nó vào thì mới dùng được
- Dùng function khi viết trong class
```js
constructor(props) {
  super(props);
  this.state = {
    username: "", // state lưu lại username
  };
  this.handleOnChangeName = this.handleOnChangeName.bind(this);
}
handleOnChangeName(event) {
  // => bắt buộc phải bind con trỏ this vào thì nó mới hiểu (bind vào trong constructor)
  this.setState({ username: event.target.value });
}
```
- Dùng arrow function
```js
handleOnChangeName = (event) => {
  // => không cần bind mà js nó tự hiểu luôn.
  this.setState({ username: event.target.value });
}
```
</markdown>
</details>

<details close>
<summary>Input and Submit form</summary>
<markdown>
- define
```js
import React from "react";

class App6 extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      username: "", // state lưu lại username
      password: "", // state lưu lại password
    };

    this.handleOnChangeName = this.handleOnChangeName.bind(this);
    this.handleOnChangePassword = this.handleOnChangePassword.bind(this);
    this.handleOnSubmit = this.handleOnSubmit.bind(this);
  }
  
  handleOnChangeName(event) {
    // handle sự kiện người dùng gõ vào ô username
    this.setState({ username: event.target.value });
  }
  handleOnChangePassword(event) {
    // handle sự kiện người dùng gõ vào ô password
    this.setState({ password: event.target.value });
  }
  handleOnSubmit(event) {
    // handle sự kiện người dùng ấn submit
    event.preventDefault(); // thông thường khi ấn vào nút submit của form thì form sẽ gửi request tới server và reset form => ta cần chặn lại sự kiện gốc của nó để tránh reset form
    console.log("On Submit", this.state);
  }
  render() {
    return (
      <div>
        <div>Form Controll</div>
        <form onClick={this.handleOnSubmit}>
          <label> Username: </label>
          <input
            type="text"
            value={this.state.username} // truyền giá trị vào input
            onChange={this.handleOnChangeName} // handle onChange when user typing
          ></input>

          <label> Password: </label>
          <input
            type="text"
            value={this.state.password}
            onChange={this.handleOnChangePassword}
          ></input>

          <input type="submit" value="Submit"></input>
        </form>
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

<details close>
<summary>Text Area</summary>
<markdown>

```js
import React from "react";

class App6 extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      essay: "default message",
    };
  }

  handleOnChangeEssay = (event) => {
    console.log(event.target.value);
    this.setState({ essay: event.target.value });
  };
  handleOnSubmit = (event) => {
    event.preventDefault();
    console.log(this.state);
  };
  render() {
    return (
      <div>
        <div>Form Controll</div>
        <form onSubmit={this.handleOnSubmit}>
          <label> Essay: </label>
          <textarea
            type="text"
            value={this.state.essay}
            onChange={this.handleOnChangeEssay}
          ></textarea>
          <input type="submit" value="Submit"></input>
        </form>
      </div>
    );
  }
}

export default App6;

```
</markdown>
</details>


