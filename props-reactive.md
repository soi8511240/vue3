# Vue3 반응성 유지

```
const a = ref('1');
const b = reactive({
  name: '';
});
a.value = '2' // 반응성 유지
b['name'] = '이름' // 반응성 유지
```

### 문제점
```
const c = ref({
  name: props.name // 반응성 유지안됨
})
```

### 해결책 
```
const c = computed(()=>props.name) // 반응성 유지
```
