---

title : How to Write a Post &#45; Markdown Tutorial 2

date : 2022-07-13 16:55:00 + 0900

categories: [Github, Tutorial]

tags: [github, jekyll, chirpy, markdown]

---

## 1) Picture 

```
![alt "Figure explanation"]("File path")
```
If you want to insert caption, use `*caption*`.
 
 
 &nbsp;&nbsp;&nbsp;&nbsp;
## 2) Table

&nbsp;
### 2.1) Structure of Table

```
| First Header  | Second Header | Third Header         |  
| :------------ | :-----------: | -------------------: |
| First row     | Data          | Very long data entry |
| Second row    | **Cell**      | *Cell*               |
| Third row     | Cell that spans across two columns  ||  
[Table caption, works as a reference][section-mmd-tables-table1]
```
Results  
| First Header  | Second Header | Third Header         |    
| :------------ | :-----------: | -------------------: |  
| First row     | Data          | Very long data entry |  
| Second row    | **Cell**      | *Cell*               |  
| Third row     | Cell that spans across two columns  ||  
[Table caption, works as a reference][table1]
  
&nbsp;
### 2.2) Alignment
Insert `:` symbol one or both side of headers. 

```
| Header One | Header Two | Header Three | Header Four |    
| ---------- | :--------- | :----------: | ----------: |  
| Default    | Left       | Center       | Right       |    
```

Results  
| Header One | Header Two | Header Three | Header Four |    
| ---------- | :--------- | :----------: | ----------: |  
| Default    | Left       | Center       | Right       |      
  
&nbsp;
### 2.3) Column Spanning

```
| Column 1 | Column 2 | Column 3 | Column 4 |
| -------- | :------: | -------- | -------- |
| No span  | Span across three columns    |||  
```

Retults  
| Column 1 | Column 2 | Column 3 | Column 4 |    
| -------- | :------: | -------- | -------- |  
| No span  | Span across three columns    |||  
  

&nbsp;&nbsp;&nbsp;&nbsp;
## 3) Emphasis

```
Emphasize \*this\* // Italic
Emphasize \*\*this\*\* // Bold
Emphasize \*\*\*this\*\*\* // Bold and Italic
```
Results  
Emphasize \*this\*   
Emphasize \*\*this\*\*  
Emphasize \*\*\*this\*\*\*   


&nbsp;&nbsp;&nbsp;&nbsp;
## 4) Link

```
[Google](http://www.google.com) // Inline
Google[1] is a search engine. // Reference
[1]: http://google.com 
<http://www/google.co.kr> // url
```
Results  
[Google](http://www.google.com)  
Google[1] is a search engine.   
[1]: http://google.com
<http://www.google.com>   


