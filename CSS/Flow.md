# Flow

in flow
기본적으로 html element는 위에서 아래로, 왼쪽에서 오른쪽으로 가는 Flow를 가지게 된다.

out of flow
하지만 CSS의 특정 Properties는 이러한 기존의 flow에서 벗어날 수 있도록 해준다.

- float
- position: absolute, fixed

float와 absolutely position은 기존의 flow를 벗어나게 되는데, 이러한 특성을 가지는 item은 BFC를 형성하게 된다.

## BFC (Block Formatting Context)

BFC는 "block box 레이아웃을 만들고, ploating 요소가 다른 elment와 상호작용하는 공간"으로 정의된다.

BFC를 형성하는 대표적인 예는 아래와 같다.

- html
- Float
- position: absolute, fixed
- inline-block
- overflow : auto, hidden... (visible이 아닌 값)

## Float

다시 Flow로 돌아와서 Float 속성에 대해 알아볼 것이다.
아래의 코드는 float 속성을 가지는 예이다.  
float 속성을 가지는 element는 기존의 flow에서 벗어나기 때문에, container가 이를 포함할 수 없게 된다(wrapping하지 못한다).

```html
<style>
  .container {
    background-color: rgb(224, 206, 247);
    border: 5px solid rebeccapurple;
  }
  .float {
    float: left;
    width: 200px;
    height: 100px;
    background-color: rgba(255, 255, 255, 0.5);
    border: 1px solid black;
    padding: 10px;
  }
</style>
<body>
  <div class="container">
    <div class="float">I am a floated box!</div>
    <p>I am content inside the container.</p>
  </div>
</body>
```

![float](../assets/flow_float.png)

## Position

position absolute, fixed도 BFC를 형성하기 때문에 비슷하다.
absolute와 fixed의 차이는 아래와 같다

- absolute : 자신의 가장 가까운 조상 element중에 position값을 가지는(static이 아닌) elemelnt, 없다면 초기의 containing block(root html)으로부터 위치를 정한다.
- fixed: viewport를 기준으로 위치를 정한다.

```html
<style>
  .container {
    background-color: lime;
    border: 5px solid rebeccapurple;
  }
  .absolute {
    position: fixed;
    top: 30px;
    width: 200px;
    height: 100px;
    background-color: red;
    border: 1px solid black;
    padding: 10px;
  }
</style>
<body>
  <div class="container">
    <div class="absolute">I am a absolute box!</div>
    <p>I am content inside the container.</p>
  </div>
</body>
```

![absolute](../assets/flow_absolute.png)

## Float과 Absolutely Position의 차이

### Space

우선 공간 차지 여부가 차이가 난다.

Float의 경우에는 기존의 flow에서 가지는 자신의 공간을 유지한다.

위의 코드 예시에서 Float의 경우에는 Container 안에서 자신의 공간을 유지한다.

하지만 Position absolute, fixed는 기존 flow에서 자신이 차지해야하는 공간이 사라진다.
그렇기 때문에 Position의 예에서는 <div class="absolute"> 태그가 200x100 공간을 container에서 차지하지 않고, <p> 태그가 위로 올라가버린다.

float : 기존 flow에서 자신의 공간을 유지
absolutely position: 기존의 flow에서 자신의 공간이 사라짐

### Wrap

공간 차지 여부는, 위의 속성을 가진 container가 wrapping 할 수 있는가의 여부에도 차이가 생긴다.

container를 BFC로 만들어주면, BFC는 BFC를 감쌀 수 있기 때문에 자식 element를 감쌀 수 있다.  
따라서, dispay: flow-root; 혹은 overflow: visible을 제외한 다른 값(auto, hidden)을 넣어주면
자식의 float 속성을 wrapping 할 수 있다.

```css
.container {
  display: flow-root;
  /* 또는 overflow: auto; */
}
```

![float_wrap](../assets/float_wrap.png)

하지만, position의 경우에는 기존의 flow에서 자신의 space 자체가 사라지기 때문에 BFC로 감싼다고 해도
container가 자식을 wrapping할 수 없다.
