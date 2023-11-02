<template>
  <tr class="table-row"
      :style="{'grid-template-columns': columnTemplates}">
    <slot></slot>
  </tr>
</template>

<script setup>
const props = defineProps({
  columnTemplates: {
    type: String,
    required: false
  }
})
</script>

<style lang="scss" scoped>
.table-row {
  display: grid;
  column-gap: 10px;
  align-items: center;
  border-bottom: 1px solid #EAECF0;

  &:hover {
    background: #EAECF0;
    cursor: pointer;
  }

  &__items-center {
    justify-items: center;
  }
}
</style>
