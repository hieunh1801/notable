---
title: Elastic Search - Hand on
created: '2020-06-29T02:52:05.868Z'
modified: '2020-06-29T02:55:33.260Z'
---

# Elastic Search - Hand on
- bật elastic search server
- bật kibana => vào dev tool
```bash
# Indexing data
# nếu index chưa có => tự tạo

# Indexing one data 
PUT /school/_doc/3
{
  "class_name": "12A3"
}

# get data by id
GET school/_doc/1
```
