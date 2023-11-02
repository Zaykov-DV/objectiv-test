<template>
  <table class="table">
    <thead class="table__head"
           :style="{'grid-template-columns': columnTemplates}">
    <tr class="table__name"
        v-for="(element, value, i) of head"
        :key="i"
        @click="clickOnHead(element, value)">
      <td>{{ element }}</td>
      <div class="table__sort">
        <IconBase class="table__icon" :class="{'is-active': currentSortDir === 'asc' && currentSort === value}" width="10" height="10">
          <IconSort />
        </IconBase>
        <IconBase class="table__icon" :class="{'is-active': currentSortDir === 'desc' && currentSort === value }" width="10" height="10">
          <IconSort />
        </IconBase>
      </div>
    </tr>
    </thead>
    <tbody class="table__body">
      <slot></slot>
    </tbody>
  </table>
</template>

<script setup>
import IconBase from "@/components/UI/IconBase.vue";
import IconSort from "@/components/icons/IconSort.vue";

const props = defineProps({
  head: {
    type: Object,
    required: false
  },
  columnTemplates: {
    type: String,
    required: false
  },
  currentSortDir: {
    type: String,
    required: false
  },
  currentSort: {
    type: String,
    required: false
  }
})

const emit = defineEmits(['sorting'])

const clickOnHead = (_, value) => {
  emit('sorting', value.toLowerCase())
}
</script>


<style lang="scss" scoped>
.table {
  position: relative;
  display: flex;
  flex-direction: column;
  background-color: #fff;
  max-width: max-content;
  width: 100%;
  max-height: 400px;
  height: 100%;

  &__head {
    position: sticky;
    top: 0;
    width: 100%;
    display: grid;
    column-gap: 10px;
    align-items: center;
    border-bottom: 1px solid #EAECF0;
    background: #F9FAFB;
  }

  &__name {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px 24px;
    color: #667085;
    font-size: 12px;
    font-style: normal;
    font-weight: 500;
    line-height: 18px;
    cursor: pointer;
  }

  &__body {
    overflow-y: scroll;
    &::-webkit-scrollbar {
      width: 7px;
    }

    &::-webkit-scrollbar-track {
      background: #f1f1f1;
      border-radius: 25px;
    }

    &::-webkit-scrollbar-thumb {
      background: #ccc;
      border-radius: 25px;
    }
  }

  &__sort {
    display: flex;
    flex-direction: column;
  }

  &__icon {
    &:first-child {
      rotate: 180deg;
      translate: -6px -3px;
    }

    &.is-active {
      fill: #29277d;
      stroke: #29277d;
    }
  }
}
</style>
