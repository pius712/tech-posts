# 기본 개념 훑고 넘어가기

정말 기본은 안다는 가정하에 작성된 포스트입니다.  
첫 번째 포스트는 다들 알지만, 놓치기 쉬운 개념들을 짚고 넘어가고자 합니다.

- viewport
- Box model
- 공백문자
- max-width, margin-left, margin-right

## Viewport


## Box model

box-sizing : content-box | border-box


### content-box

`box-sizing = content-box` : 

CSS 표준에 의하면 이것이 기본값이다. 이는 width, height가 해당 태그의 콘텐츠 영역만을 포함한다. 
만약, border, padding 값이 있다면 그 값은 콘텐츠의 width, heigth에 추가된다.  
즉, 4개의 box가 각각 `{ width: 25% }`라고 한다면, 하나의 box라도 border, padding이 들어가는 순간 부모 컨텐츠를 넘겨버리는 결과가 생긴다. 

### border-box

`box-sizing: border-box` 
```css
.my-component{
  width : 300px;
  padding: 20px;
  border: 10px solid gray;
  margin: 10px;
}
```
my-component의 속성이 위와 같다면, 이 경우에는 width의 값 300px는 컨텐츠의 너비 + padding 값 + border 값을 합친것이다.   
만약, width=100% 를 준 다음 margin:10px를 주면 어떻게 될까? 

우선 주의해야할 점은, 100%라는 것이 꽉 채운다는 의미가 아니다. 100%는 비율적으로 볼 때, 같은 크기라는 뜻이다. 
그렇기 때문에, parent| margin | children의 순으로 진행되어, parent와 같은 크기를 차지하고 우측의 마진을 다시 주는 방식이다.
부모 컨텐츠를 꽉채우고 사이의 빈 공간을 주기 위해서 width:100% + margin을 주는 일이 없도록 하자. 

## 공백문자

종종 하나의 라인에 여러 개의 box를 배치할 때, 크기가 100%임에도 불구하고 다음 라인으로 넘어가는 경우가 있다.
아래의 예시는 코드로 봤을때, 2개의 section 태그가 하나의 라인에 있을 것이라고 생각하지만, 실제로는 그렇지 않다.

왜 그런것일까? 바로 공백문자때문이다.
section태그와 section태그 사이에는 공백문자가 존재하는 것이다. 이 공백문자가 차지하는 영역때문에, 100%를 넘어버리는 것이다. 

```html
<div class="container">
  <section class="item item-a">lorem...</section> <!-- 다음 section까지 공백문자-->
  <section class="item item-b">lorem...</section>
</div>
```

```css
*{
  box-sizing: border-box;
}
.item {
  display: inline-block;
}
.item-a{
  width: 40%;
  background-color: blue;
}
.item-b{
  width: 60%;
  background-color: red;
}
}
```

### 해결책

그렇다면 이 문제를 해결할 수는 없을까? 

1. 태그사이를 붙여버린다. 

아래와 같이 태그 사이를 붙여버리는 방법도 있지만, 코드의 가독성이 떨어지기 때문에 바람직하지 않다.

```html
<section></section><section></section>
```

2. font-size : 0

폰트 사이즈를 0을 주게 되면, 공백문자의 사이즈가 0이기 때문에 하나의 라인으로 붙게 된다.  
하지만, 아래에 해당하는 모든 태그가 적용을 받아서 글을 볼 수 없게되는데, 다른 태그에 font-size를 주어야 한다.

## max-width, margin-left, margin-right

`max-width` 단순히 최대 너비인가? 

브라우저의 크기가 변할때, 일반적인 블럭(block) 단위의 태그들은 브라우저의 크기가 늘어나면 따라서 늘어나게 된다.  
하지만, container의 max-width가 1000px이면 브라우저가 1000을 넘어가는 순간, 해당 컨테이너는 1000px에서 멈추게 된다.

```css
.container{
  max-width: 1000px
}
```

컨테이너 내부의 자식 elment가 브라우저의 크기가 1000 이상일때 가운데 정렬을 두고 싶다면 어떻게 하면 될까?
좌,우측에 마진을 auto로 정해주면 1000px가 넘어갔을때 마진 | 컨텐츠 | 마진 과 같은 방식으로 가운데 정렬이 된다.

```css
.container{
  max-width: 1000px;
  margin-left: auto;
  margin-right: auto;
}
```

헤더의 네비게이션에서 종종 좌측상단의 로고와 오른쪽 상단의 탭들을 표현할 때, margin-left:auto와 같은 값들이 사용된다. 


