# Vue3 반응성 유지

<pre><code>
const a = ref('1');
const b = reactive({
  name: '';
});
a.value = '2' // 반응성 유지
b['name'] = '이름' // 반응성 유지
</code></pre>

### 문제점
<pre><code>
const c = ref({
  name: props.name // 반응성 유지안됨
})
</code></pre>

### 해결책 
<pre><code>
const c = computed(()=>props.name) // 반응성 유지
</code></pre>
