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
    ghostClass="sortable-ghost"
	  chosenClass="sortable-chosen"
	  dragClass="sortable-drag"
    :animation="200"
  >
    <template #item="{element}">
      <div
        class="draggable-item"
        :class="[element.type]"
        @click="handleItemClick(element)"
        v-if="disableDraggable"
      >
        <component :is="getComponentElement(element.type)" v-bind="element.value"></component>
      </div>
      <InEdit v-else v-model="element.type" :title="element.value.title"></InEdit>
    </template>
  </draggable>

  <div class="button-area">
    <button @click="handleToggleDraggable">Toggle Draggable</button>
  </div>
  
</template>

<script lang="ts">
import { defineComponent, isRef, reactive, ref, toRaw, unref } from 'vue'
import draggable from 'vuedraggable'

import HelloWorld from './components/HelloWorld.vue'

import InEdit from './components/widget/InEdit.vue'

// dynamic component 
import DynamicComp1 from './components/DynamicComp1.vue'
import DynamicComp2 from './components/DynamicComp2.vue'

export default defineComponent({
  name: 'App',
  components: {
    HelloWorld,
    draggable,
    InEdit,
    
    // dynamic
    DynamicComp1,
    DynamicComp2,
  },
  setup() {
    const draggableItems = ref([
        {
          id: 1,
          value: {
            title: 'mock1',
            name: 'Mock 1',
          },
          type: 'type1',
        },
        {
          id: 2,
          value: {
            title: 'mock2',
            name: 'Mock 2',
          },
          type: 'type1',
        },
        {
          id: 3,
          value: {
            title: 'mock3',
            name: 'Mock 3',
          },
          type: 'type1',
        },
        {
          id: 4,
          value: {
            title: 'mock4',
            name: 'Mock 4',
          },
          type: 'type1',
        },
      ]);
    
    const disableDraggable = ref(true);

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

    const getComponentElement = (type) => {
      return type = (type === 'type1') ? DynamicComp1 : DynamicComp2
    }

    return {
      disableDraggable,
      draggableItems,
      handleDragEnd,
      handleItemClick,
      handleToggleDraggable,

      getComponentElement
    }
  }
})
</script>

<style>
h1, h2, h3, h4, h5, h6 {
  margin: 0;
}
p {
  margin: 0;
}
</style>

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
  display: block;
  background: #fff;
}

.draggable-item.sortable-ghost {
  background: rgb(88.2%, 92.9%, 100%)
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