<script setup>
import {ref} from 'vue'
import Select from "@/components/UI/Select.vue";

const options = ref([
  {
    id: 1,
    title: 'Слон'
  },
  {
    id: 2,
    title: 'Бегемот'
  },
  {
    id: 3,
    title: 'Зебра'
  },
  {
    id: 4,
    title: 'Жираф'
  },
  {
    id: 5,
    title: 'Лев'
  }

])
const parentSelectedOption = ref(null)
</script>

<template>
  <h1>Select</h1>
  <Select :options="options" v-model="parentSelectedOption"/>
  <div>Selected option: {{ parentSelectedOption }}</div>
</template>

<style scoped lang="scss">

</style>
