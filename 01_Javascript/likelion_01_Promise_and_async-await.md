## Promise

언젠간 해결될 것이라는 약속이다. callback의 경우 중첩되면 가독성이 좋지않고 callback hell 문제가 발생하여 등장한 개념이다.

```js
function greeting(){
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log("HI~")
            resolve("good")
        }, 1000)
    })
}

greeting()
.then((arg) => console.log(arg))
// catch도 동일하게 사용가능하다.
```

### resolve

해결, 성공했다는 결과로 then으로 향하게 된다.

### reject

거절, 실패했다는 결과로 정상적으로 해결되지 않았다는 것을 뜻한다. 이는 catch로 향하게 된다.



## Async-Await

프로미스 객체는 아니나, then을 더 직관적이고 간편하게 쓸 수 있도록 도와주는 동일한 기능이다.

then과 catch의 사용을 더 편리하게 하기위해 등장한개념이다.

```js
async func(arg) {
    const res = await get_result() // 이녀석이 결과를 뱉을 때까지 기다리겠다.
}
```

