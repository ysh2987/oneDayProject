## Vue는 왜 props 변경시 컴포넌트 재 렌더링 안될까?

- react의 경우 props가 변경되면 컴포넌트가 재 렌더링

- vue의 경우 props가 변경되어도 컴포넌트가 재 렌더링 되지 않음


## data 메서드

- data 속성은 반응형 모델을 선언할 때 사용한다.

- 반응형 모델이란 어떤 액션으로 인해 값이 변경되었을 때 자바스크립트와 사용자가 보는 뷰에서 보이는 값도 같이 연동되어 변경되는 것을 의미한다.


```javascript 
export default {

 props: {
    selectUser: Object,
    selectCompany: Object,
  },

  data() {
    // 렌더링 될때 처리할 로직
  },
}


```
```vue
<template>
  {{userParsing }}
  {{companyParsing }}
</template>
```

- 하지만 props가 변경되어도 화면에 렌더 되지 않음


## 원인
- props 형태가 object이기 때문에 object 내부에 데이터가 변경되어도 참조하는 주소값이 같기 떄문에 변경이 감지가 되지 않음

## 해결 방법 - watch
- watch는 뷰 인스턴스 내의 데이터의 변화를 감지하여 특정 로직을 수행해야 할 때 사용하는 감시자 속성

```javascript
watch: {
    selectCompany() {
     // 처리할 로직
    }
```

- 위와 같이 selectCompany 내부의 데이터가 변경될 때 변경을 감시하는 watch 메서드를 사용



## 해결 방법 - setup(props)
- data 메소드 정의 / watch 메서드 정의 너무 번거로움
- vue3 에서 setup 메서드 업데이트

```javascript
 setup(props) {
	const { title } = toRefs(props)
	console.log(title.value)
}
```

- 추후 학습이 필요....
