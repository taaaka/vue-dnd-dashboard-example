<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Hello Vue 3 + TypeScript + Vite" />
  <hr>
  <draggable 
    v-model="draggableItems" 
    group="people" 
    item-key="id"
    @end="handleDragEnd"
  >
    <template #item="{element}">
      <div>value is : {{element.value}}</div>
    </template>
  </draggable>
</template>

<script lang="ts">
import { defineComponent, isRef, reactive, ref, toRaw, unref } from 'vue'
import HelloWorld from './components/HelloWorld.vue'

import draggable from 'vuedraggable'

export default defineComponent({
  name: 'App',
  components: {
    HelloWorld,
    draggable,
  },
  setup() {
    const draggableItems = ref([
        {
          id: 1,
          value: 'aaa',
        },
        {
          id: 2,
          value: 'vvv',
        },
        {
          id: 3,
          value: 'ccc',
        },
        {
          id: 4,
          value: 'aaasdfasdfa',
        },
      ]);

    const handleDragEnd = () => {
      
      console.log(toRaw(draggableItems.value).map(v => toRaw(v)));
    };

    return {
      draggableItems,
      handleDragEnd,
    }
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>