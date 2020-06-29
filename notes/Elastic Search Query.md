---
tags: [Notebooks/Coding Technology/Elastic Search]
title: Elastic Search Query
created: '2020-06-23T08:33:14.043Z'
modified: '2020-06-23T09:01:39.077Z'
---

# Elastic Search Query
- Mở kibana => thanh tab bên trái => Dev Tools
- Search API https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-body.html

<details close>
<summary>Create Index</summary>
<markdown>
```bash
PUT school # create an Index
```
</markdown>
</details>


<details close>
<summary>Add data to Index</summary>
<markdown>
```bash
# _doc: là type
# 16: là id. Nếu tồn tại id rồi thì ta sẽ được update
POST school/_doc/16
{
   "name":"Crescent School", "description":"State Board Affiliation",
   "street":"Tonk Road",
   "city":"Jaipur", "state":"RJ", "zip":"176114","location":[26.8535922,75.7923988],
   "fees":2500, "tags":["Well equipped labs"], "rating":"4.5"
}
```
</markdown>
</details>

<details close>
<summary>Query by Request Data</summary>
<markdown>
```bash
# query field of school => trả về thông tin các field của school
GET school

# query data of school
GET school/_search 
# tương đương: select * from school

# query data that match
GET GET school/_search?q=_type:"_doc" 
# tương đương: select * from school where _type = "_doc"
```
</markdown>
</details>


<details close>
<summary>Query by Request Body</summary>
<markdown>
```bash
# query field of school => trả về thông tin các field của school
GET school

# query data of school
GET school/_search 
# tương đương: select * from school

# query data that match
GET GET school/_search?q=_type:"_doc" 
# tương đương: select * from school where _type = "_doc"
```
</markdown>
</details>
