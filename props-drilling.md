props drilling

<!-- A 컴포넌트 -->
<template>
  <B :propA="valueA" :propB="valueB" customAttr="hello" @customEvent="handler" />
</template>

<script setup>
import { ref } from 'vue';
import B from './B.vue';

const valueA = ref('값A');
const valueB = ref('값B');

const handler = () => {
  // 이벤트 처리 로직
};
</script>



<!-- B 컴포넌트 -->
<template>
  <div>
    <C v-bind="$attrs" />
  </div>
</template>

<script setup>
import { useAttrs } from 'vue';
import C from './C.vue';

// $attrs에 접근하기 위해 useAttrs 훅 사용
const attrs = useAttrs();
/*attrs {
  propA: '값A',
  propB: '값B',
  customAttr: 'hello',
  onCustomEvent: [Function: handler]
}*/

// inheritAttrs: false 설정을 위해 defineOptions 매크로 사용
// 참고: defineOptions는 Vue 3.3+ 버전에서 사용 가능합니다.
defineOptions({
  inheritAttrs: false
});
</script>




장점: 

1. 속성 전달: $attrs는 부모 컴포넌트에서 전달받은 모든 속성(props로 명시적으로 선언되지 않은 속성들)을 포함합니다. v-bind="$attrs"를 사용하면 이러한 모든 속성을 자식 컴포넌트(여기서는 C 컴포넌트)로 한 번에 전달할 수 있습니다.


2. 코드 간소화: 각 속성을 개별적으로 전달하는 대신 한 줄로 모든 속성을 전달할 수 있어 코드가 간결해집니다.


3. 유연성: B 컴포넌트가 어떤 속성을 받을지 미리 알 필요가 없습니다. A 컴포넌트에서 전달하는 모든 속성이 자동으로 C 컴포넌트로 전달됩니다.


4. 투명한 래퍼 컴포넌트: B 컴포넌트가 단순히 A와 C 사이의 중간 역할을 하는 경우, 이 방식을 통해 B 컴포넌트를 "투명한" 래퍼로 만들 수 있습니다.

 

5. 컴포넌트 간 의존성이 명시적으로 드러납니다.

 

6. 작은 규모의 애플리케이션에서는 간단하고 직관적입니다.

inheritAttrs: false 옵션과 함께 사용하면, B 컴포넌트의 루트 요소에 불필요한 속성이 적용되는 것을 방지하면서도 원하는 자식 컴포넌트(C)에게 모든 속성을 전달할 수 있습니다.


이 방식은 특히 고차 컴포넌트(HOC) 패턴이나 컴포넌트 구성을 할 때 유용하지만, 경우에 따라선 안티패턴이

될 수도 있습니다.


단점:


1. 깊은 컴포넌트 트리에서는 유지보수가 어려워질 수 있습니다.


2. 중간 컴포넌트들이 불필요한 props를 전달하게 됩니다.


3. 코드의 가독성이 떨어질 수 있습니다.


4. 컴포넌트 재사용성이 떨어질 수 있습니다.


다음과 같은 경우에는 props drilling을 피하는 것이 좋습니다
1. 컴포넌트 트리가 깊고 복잡할 때
2. 여러 컴포넌트에서 동일한 데이터에 접근해야 할 때
3. 중간 컴포넌트들이 전달만 하고 사용하지 않는 props가 많을 때

이러한 상황에서는 다음과 같은 대안을 고려할 수 있습니다:
//1. Vuex나 Pinia 같은 상태 관리 라이브러리 사용
//2. Provide/Inject API 사용
3. Composition API와 컴포지션 함수를 활용한 로직 분리
4. 이벤트 버스 또는 옵저버 패턴 사용 (복잡성 주의)
