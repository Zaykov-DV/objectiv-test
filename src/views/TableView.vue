<script setup>
import {ref, computed} from 'vue'
import BaseTable from '@/components/UI/Table/BaseTable.vue'
import TableRow from '@/components/UI/Table/TableRow.vue'
import TableColumn from '@/components/UI/Table/TableColumn.vue'

const tableHeadsRef = ref({
  number: 'Номер',
  developer: 'Девелопер',
  deadline: 'Срок',
  type: 'Тип',
  floor: 'Этаж',
  square: 'Площадь'
})
const tableHeads = () => {
  return tableHeadsRef.map((item) => {
    return item.value
  })
}
const tableSizeColumns = '100px 200px 150px 150px 100px 150px'

const data = ref([
  {
    id: 1,
    number: 421,
    developer: 'PRINZIP',
    deadline: '2005-08-09T18:31:42',
    type: 'Студия',
    floor: 2,
    square: 100.3
  },
  {
    id: 2,
    number: 73,
    developer: 'Брусника',
    deadline: '2005-08-09T18:31:42',
    type: '2-к',
    floor: 2,
    square: 10.3
  },
  {
    id: 3,
    number: 122,
    developer: 'TEN',
    deadline: '2005-08-09T18:31:42',
    type: '3-к',
    floor: 2,
    square: 103
  },
  {
    id: 4,
    number: 1,
    developer: 'PRINZIP',
    deadline: '2005-08-09T18:31:42',
    type: 'Студия',
    floor: 2,
    square: 100.3
  },
  {
    id: 5,
    number: 72,
    developer: 'Брусника',
    deadline: '2005-08-09T18:31:42',
    type: '2-к',
    floor: 2,
    square: 10.3
  },
  {
    id: 6,
    number: 23,
    developer: 'TEN',
    deadline: '2005-08-09T18:31:42',
    type: '3-к',
    floor: 2,
    square: 103
  },
  {
    id: 7,
    number: 5,
    developer: 'PRINZIP',
    deadline: '2005-08-09T18:31:42',
    type: 'Студия',
    floor: 2,
    square: 100.3
  },
  {
    id: 8,
    number: 2,
    developer: 'Брусника',
    deadline: '2005-08-09T18:31:42',
    type: '2-к',
    floor: 2,
    square: 10.3
  },
  {
    id: 9,
    number: 97,
    developer: 'TEN',
    deadline: '2005-08-09T18:31:42',
    type: '3-к',
    floor: 2,
    square: 103
  },
  {
    id: 10,
    number: 34,
    developer: 'PRINZIP',
    deadline: '2005-08-09T18:31:42',
    type: 'Студия',
    floor: 2,
    square: 100.3
  },
  {
    id: 11,
    number: 1,
    developer: 'Брусника',
    deadline: '2005-08-09T18:31:42',
    type: '2-к',
    floor: 2,
    square: 10.3
  },
  {
    id: 12,
    number: 88,
    developer: 'TEN',
    deadline: '2005-08-09T18:31:42',
    type: '3-к',
    floor: 2,
    square: 103
  }
])

// Sorting
const currentSort = ref('number')
const currentSortDir = ref('asc')

const tableSorting = computed(() => {
  return data?.value.sort((a, b) => {
    let modifier = 1;
    if (currentSortDir.value === 'desc') modifier = -1;
    if (a[currentSort.value] < b[currentSort.value]) return -1 * modifier;
    if (a[currentSort.value] > b[currentSort.value]) return 1 * modifier;
    return 0;
  })
})

const setSort = (sortKey) => {
  console.log(sortKey)
  if (sortKey === currentSort.value) {
    currentSortDir.value = currentSortDir.value === 'asc' ? 'desc' : 'asc';
  }
  currentSort.value = sortKey;
}
</script>

<template>
  <h1>Table</h1>
  <BaseTable class="table"
      :head="tableHeadsRef"
      :columnTemplates="tableSizeColumns"
      :currentSortDir="currentSortDir"
      :currentSort="currentSort"
      @sorting="setSort">
    <TableRow
        v-for="item in tableSorting"
        :key="item.id"
        :columnTemplates="tableSizeColumns">
      <TableColumn>{{ item.number }}</TableColumn>
      <TableColumn>{{ item.developer }}</TableColumn>
      <TableColumn> {{
          new Date(item.deadline).toLocaleString('en-EU', {year: 'numeric', month: 'long', day: 'numeric'})
        }}
      </TableColumn>
      <TableColumn>{{ item.type }}</TableColumn>
      <TableColumn>{{ item.floor }}</TableColumn>
      <TableColumn>{{ item.square }}</TableColumn>
    </TableRow>
  </BaseTable>
</template>
