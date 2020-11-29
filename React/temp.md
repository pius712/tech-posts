


컴포넌트의 아래와 같이 이름은 지어주는 것이 좋다.
이름을 적지 않으면 컴포넌트의 이름이 anonymous로 개발자 도구에서 나오기 때문에
디버깅하기가 어렵다. 


```js
export default function ComponentName(){


}
```

컴포넌트 바깥의 변수들은 가장 아래에 작성해주는 것이 가장 좋다.
그렇지 않으면 코드의 가독성이 올라간다.

컴포넌트 내부에서 변수를 정의하면 렌더링 할때마다 이를 사용하여 객체나 변수를 만들기 때문에, 
컴포넌트 바깥에 만드는 것이 좋다.


서로 연관된 코드끼리 모아두는 것이 가장 좋다.

예를 들어서, state / callback / useEffect 순으로 적는 것보다는, 
연관되어있는 state, callback, useEffect 를 모아서 적는 것이 가독성 측면에서도 좋고, 
이후에 훅을 만들기도 좋다.


```js
// bad 
const [user, setUser] = useState(null);

const [post, setPosts] = useState();

useEffect(()=> {
	// ...
})

// good
const [user, setUser] = useState(null);
useEffect(()=> {
	// ...
})

const [post, setPosts] = useState();
```


관심사의 분리

연관된 컴포넌트끼리 폴더를 만들어주면 좋다.

페이지별로 폴더를 만들 수 도 있다.


재사용성이 좋은 컴포넌트(state가 없는 컴포넌트) / 재사용성이 좋지 않은 컴포넌트로 분리한다.