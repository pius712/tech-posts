# Reusable Component

컴포넌트가 재사용 되기 위해서는 범용성이 있어야 하고, 비즈니스 로직이 많아지면 안된다.

## Button

기본적으로 재사용 가능한 컴포넌트를 만들기 위해서는 해당 컴포넌트가 제네릭하게 사용될 수 있도록 설계 단계에서 고려해야한다.

일반적으로 아주 작은 단위의 컴포넌트를 만들 때는, React.forwardRef()를 사용하는데, 이는 상위의 컴포넌트에서 ref를 만들어서 전달할 수 있는데, 함수형 컴포넌트에서는 ref를 받기 위해서는 해당 함수로 감싸주어야하기 때문이다.

그리고 props를 정의해주어야 한다.

### children

children을 받아주는 이유는 composition이 가능해야하기 때문이다.
아래의 경우 Button 컴포넌트에 children이 없으면 '제출'이 렌더링 되지 않는다.

```js
	return (
		<div>
			<Button>제출</Button>
		</div>
```

### className

className은 상위 컴포넌트에서 스타일을 넘겨주는 경우에 필요하다.
리액트에서는 className으로 스타일을 넣어준다.

컴포넌트를 만들때도, 이와 통일성을 줄 수 있도록 className props를 사용하는 것이 좋다.

이는 css, scss 뿐만 아니라 css-in-js 의 경우에도 해당된다.

styled-component를 사용하는 경우 컴포넌트에 스타일을 주기 위해 styled(Component)와 같은 방식을 사용할 수 있다. 이렇게 작성된 스타일은 Button 컴포넌트에 className 프로퍼티로 css class 선택자가 전달된다.

---

```js
const CustomButton = styled(Button)`
  background-color: blue;
`;
```

하지만 하위 컴포넌트에서 이 props를 받지 않는다면, style이 적용이 안된다. 따라서 아래와 같이 className을 작성해주어야 한다.

```js
export default function Button({ children, className }) {
  return <button className={className}>{children}</button>;
}
```

### ...rest

...rest의 경우는 비구조화 할당 문법에 의해서 명시하지 않은 프로퍼티의 집합이다.

```js
const Button = (props, ref) => {
  const { type, className, chilren, ...rest } = props;
  // ... 생략
};

export default React.forwardRef(Button);
```
