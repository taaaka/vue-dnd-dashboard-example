<template>
  <div>
    <h2>Dynamic Comp: {{title}}</h2>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'DynamicComp1',
  props: {
    title: {
      type: String,
      required: true,
    }
  }
})
</script>