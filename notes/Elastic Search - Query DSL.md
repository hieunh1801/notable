---
attachments: [Clipboard_2020-08-12-10-48-18.png]
title: Elastic Search - Query DSL
created: '2020-08-12T02:48:34.256Z'
modified: '2020-08-12T03:48:19.552Z'
---

# Elastic Search - Query DSL
`12/08/2020`
https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html

- DSL - viết tắt của Domain Specific Language. Elastic Search lưu data dưới dạng JSON => làm sao để truy vấn được?. Ta không thể sử dụng truy vấn SQL thuần túy được. Thay vào đó ta sử dụng DSL. DSL giống việc ta mô tả một Abstract Syntax Tree. Khi document nào có mô tả gần giống với của ta thì nó sẽ trả về kết quả

## DSL gồm 2 loại mệnh đề truy vấn
1. Leaf query clasuse: tìm kiếm giá trị cụ thể trên trường cụ thể. ví dụ: 
  - <mark>match</mark>: khớp với cái gì đó 
  - <mark>term</mark>: có luật như nào
  - <mark>range</mark>: nằm trong một phạm vi nào đó
2. Coumpound query clause: bọc lại các Leaf query clause hoặc Compound Query Clasue khác => để giúp truy vấn của ta có thêm nhiều logic. Ví dụ:
  - <mark>bool</mark>
  - <mark>dis_max</mark>
> Các mệnh đề truy vấn ở trên thực hiện khác nhau phụ thuộc vào ngữ cảnh __Query__ hoặc ngữ cảnh __Filter__ sẽ được bàn luận kế tiếp

## Ngữ cảnh Query và Filter là gì?
### Relevance Score: điểm phù hợp 
- Mặc định, Elasticsearch sắp xếp kết quả tìm kiếm phù hợp bởi relevance score, điểm này được do lường bởi độ phù hợp của document với query. Relevance Score: có giá trị từ 0 tới 1, được trả về trong metadata <mark>_score</mark> khi truy vấn. 
- Cách tính Revelance Score: để tính điểm này => phụ thuộc vào mệnh đề query chạy trong __Query Context__ hay __Filter Context__

### Query Context
- __Query context__: trả lời cho câu hỏi - Mức độ phù hợp của document với truy vấn.
  + Nghĩa là document có thể phù hợp hoặc không phù hợp
  + Hoặc có một mức độ liên quan nào đó được tính bởi __revelance score__ được thể hiện ở trường <mark>_score</mark>
- Sử dụng query context:
  + Bất cứ khi nào ta thấy từ khóa <mark>query</mark> trong câu truy vấn thì các mệnh đề trong đó được tính là ở trong __Query Context__

### Filter Context
- Filter context: mục đích của filter là lọc dữ liệu. Ví dụ A có thỏa mãn điều kiện x không. có thì lấy ra còn không thì không. Câu trả lời rất đơn giản __Yes__ or __No__. Do đó không có điểm nào được tính ở đây cả <mark>NO RELEVANCE SCORE</mark>
- Ví dụ:
  - Document này được create trong khoảng 2019 đến 2020 (lấy timestamp compare với 2019 và 2020 nếu đúng thì lấy không thì thôi. không có relevance score gì hết)
  - Document này có status = 0 hoặc status = 1
- Các filter thường được sử dụng sẽ được cache tự động bởi Elastic Search để tăng performance.
- Sử dụng ngữ cảnh filter: cứ khi nào sử dụng từ khóa <mark>filter</mark> => đó chính là filter context


### Ví dụ sử dụng query context và filter context
![](@attachment/Clipboard_2020-08-12-10-48-18.png)

