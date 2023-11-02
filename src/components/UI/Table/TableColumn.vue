<template>
  <td class="table-column">
    <span class="table-column__title" v-if="columnTitle">{{columnTitle}}: </span>
    <slot></slot>
  </td>
</template>

<script setup>
const props = defineProps({
  columnTitle: {
    type: String,
    required: false
  }
})
</script>

<style lang="scss" scoped>
.table-column {
  padding: 12px 24px;
  color: #667085;
  font-size: 14px;
  font-style: normal;
  font-weight: 400;
  line-height: 20px;
  text-align: left;
}
</style>
