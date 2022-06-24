---
title : How to Write a Post &#45; Markdown Tutorial 1
date : 2022-06-24 13:39:00 + 0900
categories: [Github, Tutorial]
tags: [github, jekyll, chirpy, markdown]
---

## 0) Write Markdown Files for Posts
The title of the .md(markdown) file for post should be ```"YYYY-MM-DD-TITLE.md"``` and locate the file in the ```_post/``` folder.
You should start your file with the contents
```
---
title : How to Write a Post - Markdown Manual 1
date : YYYY-MM-DD HH:MM:SS + 0900
categories: []
tags: [] // only in small letters
---
```
&nbsp;&nbsp;&nbsp;&nbsp;
## 1) To Enter Text
You can write text without any help of functions or symbols. 
&nbsp;&nbsp;&nbsp;&nbsp;
## 2) Title
You can write title with "#". 

```
# The biggest text.
## The second biggest text.
### The number of '#' (N) means Nth biggest text.
#### There must be a space between '#' and text.
```

Results 
# The biggest text.
## The second biggest text.
### The number of '#' (N) means Nth biggest text.
#### There must be a space between '#' and text.
&nbsp;&nbsp;&nbsp;&nbsp;
## 3) Code Block
There are two ways to use code block in your text.

### First - Use "tab" on your keyboard
```
Normal Text
// enter : You should type "enter key" before what you want to make as code block.
	codeblock
// enter : You should type "enter key" after what you want to make as code block.
Normal Text
```
Results
&nbsp;
Normal Text

	code block

Normal Text
&nbsp;&nbsp;&nbsp;&nbsp;
### Second - Use &#96;&#96;&#96;
```
\``` // Backslash is needed to remove in real code.
code block
\``` // Backslash is needed to remove in real code.
```
Result
```
code block
```
&nbsp;
If you want to use specific computational language, you should write the name of language life below.
```
\```python
print("Hello World!")
print("code block")
\```
```
Result
```python
print("Hello World!")
print("code block")
```
&nbsp;&nbsp;&nbsp;&nbsp;
## 4) BlockQuote
```
> Hello
>> World!
>>> Blockquote
```
Result
> Hello
>> World!
>>> Blockquote
&nbsp;&nbsp;&nbsp;&nbsp;
## 5) Ordered List
```
1. Hello
2. World!
3. Ordered List
```
1. Hello
2. World!
3. Ordered List
&nbsp;&nbsp;&nbsp;&nbsp;
## 6) Unordered List
You can use ```+,*,-```. The results are all same no matter which symbol you use.
```
+ Hello
	+ World! // Use "Tab key" if you want to make dependent bulltes. 
		+  Unordered List
```
Result
+ Hello
	+ World! // Use "Tab key" if you want to make dependent list. 
		+  Unordered List
