<template>
  <h1>
    Draggable Example
  </h1>
  <div class="draggable-area">
    <draggable 
      v-model="draggableItems" 
      item-key="id"
      @end="handleDragEnd"
    >
      <template #item="{element}">
        <div class="draggable-item">
          value is : {{element.value}}
        </div>
      </template>
    </draggable>
  </div>
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

<style scoped>
.draggable-area {
  width: 80vw;
  margin: auto;
  border: 2px dashed rgb(117, 164, 250);
  border-radius: 4px;
  padding: 6px;
}

.draggable-item {
  margin: 4px 0;
  padding: 10px;
  border: 1px solid rgb(50, 81, 138);
  border-radius: 4px;
}
</style>