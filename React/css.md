# CSS

## 일반적인 CSS

이름이 충돌할 수 있다. 

```js
<div className=""><div>
```

## css-module

component.module.css 파일 작성

```js
import Style from './Button.module.css`;

<div className={`${Style.button} ${Style.round}`}>
```
css 파일이 객체 형식으로 변환되면서, 객체에 hash 값을 추가해줘서 이름 충돌을 막아준다.

className을 입력을 간편하게 하기 위해서 `npm i classnames`를 설치하면 여러개의 class를 사용할 때, 편하게 사용할 수 있다. 그리고 아래와 같이 조건부 렌더링도 가능하다.

```js
import Style from './Button.module.css`;
import cn from 'classnames`;
export default function App(){

	const [isRound, setIsRound] = useState();
	render(
		<div className={cn(Style.button, {
			[Style.round] : isRound, 
			[Style.rect] : !idRound 
			})}>
		</div>
	)
}
```

## Sass

변수, 믹스인 등을 통해서 재사용이 가능하다.

`npm i node-sass`


## css-in-js

`styled-component` `emotion`