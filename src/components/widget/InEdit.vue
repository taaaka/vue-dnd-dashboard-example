<template>
  <div
    class="draggable-item"
    :class=[modelValue]
  >
    <h3>In Editing</h3>
    <label>
      <input type="radio"
        value="type1"
        v-model="typeValue"
      >
      Type1
    </label>
    <label>
      <input type="radio"
        value="type2"
        v-model="typeValue"
      >
      Type2
    </label>
  </div>
</template>

<script lang="ts">
import { defineComponent, computed } from 'vue'

type WidgetType = 'type1' | 'type2';

export default defineComponent({
  name: 'InEdit',
  props: {
    modelValue: {
      type: String,
      required: true
    },
    title: {
      type: String,
      required: true
    }
  },
  setup(props, ctx) {
    const typeValue = computed<WidgetType>({ 
      get() {return props.modelValue as WidgetType}, 
      set(value) {ctx.emit('update:modelValue', value)}
    });
    return {
      typeValue
    }
  },
})
</script>
