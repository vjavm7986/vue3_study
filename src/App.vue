<template>
  <div class="container">
    <h2>To-Do List</h2>
    <form 
      @submit.prevent="onSubmit"
      class="d-flex"
    >
      <div class="flex-grow-1 mr-2">
        <input 
          class="form-control"
          type="text" 
          v-model="todo"
          placeholder="Type new to-do"
        >
      </div>
      
      <div>
        <button 
          class="btn btn-primary" 
          type="submit"
        >
          Add
        </button>
      </div>
    </form>
    {{ todos }}
  </div>

</template>

<script>
import { ref } from 'vue';

export default {
  setup() { // vue3 composition-api 방식
    const todo = ref('');
    const todos = ref([]);
    
    const onSubmit = () => {
      // e.preventDefault(); // refresh 방지(직접 입력한 script 제외 기본 event 처리 막기) => vue에서는 @submit.prevent로 처리 가능!
      todos.value.push({
        id: Date.now(),
        subject: todo.value
      });
    };

    return {
      todo,
      todos,
      onSubmit,
      
    };
  }
}
</script>

<style>
  .name {
    color: red;
  }
</style>