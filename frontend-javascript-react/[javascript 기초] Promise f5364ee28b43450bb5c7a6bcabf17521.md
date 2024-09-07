# [javascript 기초] Promise

Tags: basic, blog, javascript
Created: 2024년 7월 28일 오후 2:20
Updated: 2024년 9월 1일 오후 5:42

## Promise 다루기

> callback에서 나타났던 callback 지옥을 해결하기 위해서 만들어진 문법으로 pending, fulfilled, rejected  의 상태를 가진다.
> 

### Promise 상태 특징

1. Promise 는 생성자로 함수를 하나 전달 받는데 executer 라고 부르며 실재로 실행 할 함수를 전달 받는다. 생성시 바로 실행 된다. 

```jsx
const promise = new Promise(()=>{
	console.log('executer');
})
```

1. executer 는 두가지 인자를 전달 받는데 resolve 와 reject 이다. resolve 는 성공시에 호출하는 함수, reject 는 실패시에 호출하는 함수이다. 

```jsx
const promise2 = new Promise((resolve, reject)=>{
	setTimeout(()=>{
		const data = {name: '미나'}
		console.log('Successfully Network request');
	}, 1000);
})
```

![image.png](%5Bjavascript%20%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A9%5D%20Promise%20f5364ee28b43450bb5c7a6bcabf17521/image.png)

1. promise 에서 성공시는 resolve 에 넘겨받은 함수를 실행한다. 

```jsx
const promise3 = new Promise((resolve, reject)=>{
	setTimeout(()=>{
		const data = {name: '미나'}
		console.log('Successfully Network request');
		resolve(data);
	}, 1000);
})

setTimeout(()=>{
	console.log('promise3: '+ promise3)
}, 2000);
// 브라우저에서 실행해 보면 fulfilled 상태 처리에 성공 했음을 알려준다.
```

![image.png](%5Bjavascript%20%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A9%5D%20Promise%20f5364ee28b43450bb5c7a6bcabf17521/image%201.png)

1.  promise 실패 했을 때는 rejected에 대항하는 함수를 호출 하도록 한다. 

```jsx
const promise4 = new Promise((resolve, reject)=>{
	setTimeout(()=>{
		const data = null
		if(data) {
			console.log('Successfully Network request');
			resolve(data);
		} else {
			reject(new Error(`Network request failed`));
		}
	}, 1000);
})

setTimeout(()=>{
	console.log('promise4: '+ promise4)
}, 2000);
```

![image.png](%5Bjavascript%20%E1%84%80%E1%85%B5%E1%84%8E%E1%85%A9%5D%20Promise%20f5364ee28b43450bb5c7a6bcabf17521/image%202.png)