<template>
  <h1>
    Draggable Example
  </h1>
  
  <draggable 
    v-model="draggableItems" 
    item-key="id"
    @end="handleDragEnd"
    class="draggable-area"
  >
    <template #item="{element}">
      <div class="draggable-item" :class=[element.type] @click="handleItemClick(element)">
        value is : {{element.value}}
      </div>
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
          type: 'type1',
        },
        {
          id: 2,
          value: 'vvv',
          type: 'type1',
        },
        {
          id: 3,
          value: 'ccc',
          type: 'type1',
        },
        {
          id: 4,
          value: 'aaasdfasdfa',
          type: 'type1',
        },
      ]);

    const handleDragEnd = () => {
      console.log(toRaw(draggableItems.value).map(v => toRaw(v)));
    };

    const handleItemClick = (item) => {
      item.type = (item.type === 'type1') ? 'type2' : 'type1'
    };

    return {
      draggableItems,
      handleDragEnd,
      handleItemClick,
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
  display: flex;
  flex-wrap: wrap;
}

.draggable-item {
  margin: 4px 0;
  padding: 10px;
  border: 1px solid rgb(50, 81, 138);
  border-radius: 4px;
  font-weight: bold;
  font-size: 20px;
  box-sizing: border-box;
}
.draggable-item.type1 {
  color: rgb(148, 71, 0);
  width: 100%;
}
.draggable-item.type2 {
  color: rgb(52, 0, 148);
  width: 50%;
}
</style>