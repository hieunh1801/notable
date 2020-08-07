---
tags: [Notebooks/Coding Technology/Reactjs]
title: 7 - List and Key rendering
created: '2020-07-27T13:08:51.926Z'
modified: '2020-07-27T13:24:50.453Z'
---

# 7 - List and Key rendering
- Hiển thị danh sách trong ReactJS
- Như đã biết thì để hiển thị một danh sách => đơn giản là ta trả về một list các component
- Trong các hàm biến đổi dữ liệu với danh sách:
  - Map: convert từ một danh sách này qua một danh sách khác
  - Reduce: làm giảm danh sách từ nhiều xuống còn ít phần tử hơn
  - Filter: lọc một danh sách để thỏa mãn điều kiện nào đó
=> chọn map để biến đổi dữ liệu

- Chú ý: Luôn cung cấp key cho các list item vì react sẽ định danh nó để khi thêm, sửa, xóa sẽ tìm tới đúng thằng để xử lý
- Sử dụng map ở đâu thì key ở đó => ko cần phải gán key vào trong ListItem
```js
import React from "react";

const students = [
  { id: 1, name: "Nam 1" },
  { id: 2, name: "Nam 2" },
  { id: 3, name: "Nam 3" },
  { id: 4, name: "Nam 4" },
  { id: 5, name: "Nam 5" },
  { id: 6, name: "Nam 6" },
];
const ListItem = ({ student }) => (
  // không cần key ở đây
  <div style={{ padding: "20px" }}>
    {student.id} : {student.name}
  </div>
);
const ListDemo = () => {
  return students.map((student) => (
    // nhớ thêm key vào đây
    <ListItem key={student.id} student={student} />
  ));
};

export default ListDemo;

```
