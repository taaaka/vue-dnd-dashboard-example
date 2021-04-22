<template>
  <div>
    <h2>(2) Dynamic</h2>
    <p>Name -> {{name}}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent, isRef, reactive, ref, toRaw, unref } from 'vue'

export default defineComponent({
  name: 'DynamicComp2',
  props: {
    name: {
      type: String,
      required: true
    }
  }
})
</script>