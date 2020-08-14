---
favorited: true
tags: [Elastic Search]
title: Elastic Search - Overview
created: '2020-06-29T02:25:29.139Z'
modified: '2020-08-12T09:40:59.872Z'
---

# Elastic Search - Overview
- Hướng dẫn cơ bản về elastic search
https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html

- Các phần mềm hỗ trợ nâng cao hơn cho elastic search
https://www.elastic.co/guide/en/elastic-stack-get-started/7.8/get-started-elastic-stack.html

- Query DSL - Domain Specific Language
https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html

- Search Query
https://www.elastic.co/guide/en/elasticsearch/reference/current/search-your-data.html

### Question
- Score khi mà ta query về có ý nghĩa gì?

### Tool Translate API
- Mở Kibana => dev tool
```bash
## Truy vấn xem chính xác chưa
POST /_sql
{
  "query" :"""
    SELECT accountMail as name, COUNT(*) as total
    FROM "workplace-chatbot-log"
    GROUP BY accountMail
  """
}

# Chính xác thì đi convert lệnh
POST /_sql/translate
{
  "query" :"""
    SELECT accountMail as name, COUNT(*) as total
    FROM "workplace-chatbot-log"
    GROUP BY accountMail
  """
}

# ở mệnh đề from ta thay bằng query
GET workplace-chatbot-log/_search
{
  "size" : 0,
  "_source" : false,
  "stored_fields" : "_none_",
  "aggregations" : {
    "groupby" : {
      "composite" : {
        "size" : 1000,
        "sources" : [
          {
            "accountMail" : {
              "terms" : {
                "field" : "accountMail.keyword",
                "missing_bucket" : true,
                "order" : "asc"
              }
            }
          }
        ]
      }
    }
  }
}
```
