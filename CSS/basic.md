---
title: CSS 기본
---

# Basic

## inherit

## inherit

기본적으로 css는 상위의 css를 상속받는다.

아래의 코드에서 item은 container의 css 속성을 상속 받게 된다.

```html
<div class="container">
  <div class="item"></div>
</div>
```

## Selector

### Basic Selector & Combinators

```css
.class1,
.class2 {
} /* 다중 선택 */
.class1 .class2 {
} /* 자손 선택 */
/* 주의) <div class='al a2'> 의 경우에는 클래스를 두개 적용한 것*/
.class1 > .class2 {
} /* 자식 선택*/
.class1 + .class2 {
} /* .class1 중에서 그 다음 선택자 .class2 선택*/
/*
	<style>
		#header h1 + p { font-size: 20px } 
	</style>
	<body>
		<div id="header">
			<h1>
			<p>
위 경우에는 #header h1 까지 접근 후에 그 다음 선택자 p의 font-size가 20px라는 뜻
*/
```

### Attribute selector (Basic Selector)

```css
[attrbute] {
}
/* 특정 proterties를 가지는 경우에 스타일 적용
	[href] { font-size: 36px}
	<a></a> 기본 font-size
	<a href="google.com"></a> font-size 36px 
 */
[attribute="value"] {
}
/*
	특정 attribute=value에 스타일을 적용
	[type='submit] { font-size: 36px}
	<button type='submit'>제출</button>
*/
```

### Pseudo

`:` -> 특정 element 기반의 선택자로, document tree에 나타나지 않는 부분에 대해서 기술한다.
`::` -> HTML의 node가 아닌 부분을 선택할 수 있다.

```css
a:link {
}
a:visited {
}
a:hover {
}
a:active {
}
a:focus {
}
```

```css
:before {
}
:after {
}
/*
	<style>
		.container:after {}
		.container:before {}
	</style>
	<div class='container>(after) 내용물 (before)</div>
*/
```
