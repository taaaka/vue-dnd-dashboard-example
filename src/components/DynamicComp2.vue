<template>
  <div>
    <h2>(2) Dynamic</h2>
    <p>title is {{title}}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent, isRef, reactive, ref, toRaw, unref } from 'vue'

export default defineComponent({
  name: 'DynamicComp2',
  props: {
    title: {
      type: String,
      // required: true
      default: 'DEFAULT'
    }
  }
})
</script>