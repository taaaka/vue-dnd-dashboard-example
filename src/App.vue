<template>
  <h1>
    Draggable Example
  </h1>
  
  <draggable 
    v-model="draggableItems" 
    item-key="id"
    @end="handleDragEnd"
    :disabled="disableDraggable"
    class="draggable-area"
    :class="{enable: !disableDraggable}"
  >
    <template #item="{element}">
      <div class="draggable-item" :class=[element.type] @click="handleItemClick(element)">
        value is : {{element.value}}
      </div>
    </template>
  </draggable>

  <div class="button-area">
    <button @click="handleToggleDraggable">Toggle Draggable</button>
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
    
    const disableDraggable = ref(false);

    const handleDragEnd = () => {
      console.log(toRaw(draggableItems.value).map(v => toRaw(v)));
    };

    const handleItemClick = (item) => {
      if (unref(disableDraggable)) {
        return;
      }
      item.type = (item.type === 'type1') ? 'type2' : 'type1'
    };

    const handleToggleDraggable = () => {
      disableDraggable.value = !unref(disableDraggable);
    }

    return {
      disableDraggable,
      draggableItems,
      handleDragEnd,
      handleItemClick,
      handleToggleDraggable
    }
  }
})
</script>

<style scoped>
.draggable-area {
  width: 80vw;
  margin: auto;
  border: 2px solid rgb(117, 164, 250);
  border-radius: 4px;
  padding: 6px;
  display: flex;
  flex-wrap: wrap;
}

.draggable-item {
  margin: 4px;
  padding: 10px;
  border: 1px solid rgb(50, 81, 138);
  border-radius: 4px;
  font-weight: bold;
  font-size: 20px;
  box-sizing: border-box;
}

.draggable-area.enable > .draggable-item {
  border-style: dashed;
}

.draggable-item.type1 {
  color: rgb(148, 71, 0);
  width: calc(100% - 8px);
}
.draggable-item.type2 {
  color: rgb(52, 0, 148);
  width: calc(50% - 8px);
}

.button-area {
  margin: 10px 0;
  text-align: center;
}

</style>