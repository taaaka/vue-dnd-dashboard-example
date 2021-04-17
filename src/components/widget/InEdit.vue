<template>
  <div
    class="draggable-item"
    :class=[modelValue]
  >
    <h4>Edit Widget</h4>
    <label>
      <input type="radio" value="type1" v-model="modelValue">
      Type1
    </label>
    <label>
      <input type="radio" value="type2" v-model="modelValue">
      Type2
    </label>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

type WidgetType = 'type1' | 'type2';

export default defineComponent({
  name: 'InEdit',
  props: {
    modelValue: {
      type: String,
      required: true
    }
  },
  setup() {},
})
</script>
