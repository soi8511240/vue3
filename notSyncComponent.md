# 비동기로 컴포넌트 처리

* [*defineAsyncComponent*](https://ko.vuejs.org/guide/components/async)


```javascript
import { defineAsyncComponent } from 'vue'

const AsyncComp = defineAsyncComponent(() => {
  return new Promise((resolve, reject) => {
    // ...서버에서 컴포넌트를 로드하는 로직
    resolve(/* 로드 된 컴포넌트 */)
  })
})
// ... 일반 컴포넌트처럼 `AsyncComp`를 사용
```
