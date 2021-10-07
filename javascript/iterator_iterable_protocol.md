# 이터러블/이터레이터 프로토콜
## 이터러블
- 이터레이터를 리턴하는 `[Symbol.iterator]()`를 가진 값
- Array, Set, Map ...
## 이터레이터
- {value, doe} 객체를 리턴하는 next() 를 가진 값
- `arr[Symbol.iterator]()`
## 이터러블/이터레이터 프로토콜
- 이터러브을 for...of, 전개 연산자 등과 함께 동작하도록한 규약
- for .. of, ...arr

## 예시 List 순회

기존 리스트 순회
```js
for (var i = 0 ; i < list.length ; i++) {
    log(list[i]);
}
```
ES6에서 리스트 순회 - 이터러블/이터레이터 프로토콜 사용
```js
for (const a of list) {
    log(a);
}
```


# 사용자 정의 이터러블
1. Symbol.iterator() 를 반환하는 객체
2. iterable 는 next를 반환해야됨
3. iterable 는 자기자신 [Symbol.iterator]을 반환해야됨.(well-formed)

```js
const iterable = {
    [Symbol.iterator]() {
        let i = 3;
        return {
            next() {
                return i == 0 ? {done: true} : {value: i--, done: false};
            },
            [Symbol.iterator]() {return this; }
        }
    }
};

let it = iterable[Symbol.iterator]();
for (const a of it) log(a);
```

# 제너레이터
- 이터레이터이자 이터러블을 생성하는 함수
- 따라서 제너레이터를 이용해서 어떠한 값도 순회할 수 있는 형태로 만들 수 있다.
- 일반 함수 명 앞에 '*'를 붙여서 선언한다.
- 제너레이터는 이터레이터 이터러블 프로토콜을 따르는 문법들과 함께 사용될 수 있다.


```js
function *gen() {
    yield 1;
    yield 2;
    yield 3;
    return 100;
}

// 순회할때는 return 값이 안 찍힘
for (const a of gen()) log(a);
```

## 제너레이터 응용
```js
function *odds(limit) {
    for (let i = 0 ; i < limit ; i++) {
        if (i % 2 == 1) yield i;
    }
}
let iter2 = odds(10);
log(iter2.next());
log(iter2.next());
.
.
.
```

```js
log([...odds(10),...odds(20)]);
const[head, ...tail] = odds(10)
log(head, tail)
```

# Reference
[함수형 프로그래밍과 JavaScript ES6+](https://www.inflearn.com/course/functional-es6/dashboard)