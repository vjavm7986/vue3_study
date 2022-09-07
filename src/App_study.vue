<template>
  <!-- vue2 방식(무조건 상위 태그로 안에를 감싸야 했음) -->
  <div> 
    <div class="name">{{ name }}</div> 
    <div class="name">{{ name1 }}</div> 
    <div>Hi</div>
  </div>

  <!-- vue3(vue2와는 다르게 root에 바로 다수의 태그로 표기 가능) -->
  <div class="name">{{ name }}</div>
  <div class="name">{{ name1 }}</div> 
  <div>Hi</div>

  <!-- vue3 함수 사용 -->
  <div class="name">
    {{ greeting('Jeff') }}
    {{ greeting(name) }}
    {{ greet }}
  </div>

  <!-- data bind -->
  <input type="text" v-bind:value="name3">
  <input v-bind:type="cType" v-bind:value="name3">
  <input v-bind:class="nameClass" v-bind:value="name3">
  <input :class="nameClass" :value="name3"> <!-- v-bind 생략 가능 -->

  <!-- vue3 이벤트 사용 -->
  <button 
    class="btn btn-primary"
    v-on:click="updateName"
  >
    Click
  </button>

  <!-- vue3 이벤트 사용(약식 : on 대신 @로 사용)-->
  <button 
    class="btn btn-primary"
    @click="updateName"
  >
    Click
  </button>




  <br>
  <!-- ========================================================================== -->
  <!-- 양방향 바인딩(v-model) : 위에는 script를 통해 화면값만 변경 가능 -->
  <!-- input 태그 내 원래 oninput이 있는데 이걸 사용함(@input) : 데이터 입력 시 발생 -->
  {{ aname }}
  <input 
    type="text" 
    :value="aname"
    @input="updateAname"
  >
  <!-- v-model로 쓰면 value binding + oninput 처리도 한번에 됨! -->
  <input 
    type="text" 
    v-model="aname"
  >
  <button 
    class="btn btn-primary"
    @click="onSubmit"
  >
    Click
  </button>
</template>

<script>
import { ref, reactive } from 'vue';

export default {
  setup() { // vue3 composition-api 방식
    let name = 'Jeff coder1'; // 변수
    const name1 = ref('Jeff coder1'); // ref 안에는 숫자, Object {}, Array [] 등도 들어갈 수 있음 / 단, Object 나 Array 는 아래와 같이 reactive로 보통 사용

    const name2 = reactive({ // 이렇게 했을 경우 id 값에 접근하려면 name2.id로 접근 가능(만약 ref라면 이렇게가 안되고 name2.value.id 이렇게 value가 필요!)
                             // reacitve는 일반 타입은 사용 못하고 오로지 Object나 Array만 가능!
      id: 1
    })
    const name3 = ref('Jeff');
    const cType = ref("number");
    const nameClass = ref("");

    const greeting = (name) => { // 함수
      return 'Hello, ' + name;
    };

    const greet = greeting(name);

    const consoleLog = () => {
      console.log('hello world');
    };

    const updateName = () => {
      name = 'Jeff coder'; // 이렇게만 했을 경우 click 시 name의 값은 바뀌지만 화면에는 안바뀜! => 일반 변수에 담으면 안된다! => ref에 담아야함!
      
      name1.value = 'Jeff coder';
      name2.id = 2;
      name3.value = 'Changed!';
      cType.value = 'text';
      nameClass.value = "name"
    };

    /////////////////////////////////////////////////////////////////////////////////////////////////////////////
    // 양방향 바인딩(v-model) 화면 값을 바꿀 때 아래 aname 값을 바꾸기!
    /////////////////////////////////////////////////////////////////////////////////////////////////////////////

    const aname = ref('Jeff');
    
    const onSubmit = () => {
      console.log(aname.value);
    };

    const updateAname = (e) => {
      console.log(e.target.value);
      aname.value = e.target.value
    };


    return {
      name,
      name1,
      name2,
      name3,
      cType,
      nameClass,
      greeting,
      greet,
      consoleLog,
      updateName,

      aname,
      onSubmit,
      updateAname,
    };
  }
}
</script>

<style>
  .name {
    color: red;
  }
</style>