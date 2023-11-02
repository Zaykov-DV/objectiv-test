<script setup>
import {ref, computed, defineProps, defineEmits, onMounted, onBeforeUnmount} from 'vue'

const emit = defineEmits(['update:modelValue'])

const props = defineProps({
  options: {
    type: Array,
    required: true
  },
  modelValue: {
    default: null
  },
  width: {
    type: String,
    default: '300px'
  }
})

const selectedOption = ref(null)

const isDropdownVisible = ref(false);

const dropdown = ref(null)
const toggleOptionSelect = (option) => {
  selectedOption.value = option;
  emit('update:modelValue', option);
  setTimeout(() => {
    isDropdownVisible.value = false
  }, 300)
}

const mappedSelectedOption = computed(() => {
  return (selectedOption.value?.title || selectedOption.value)
})

const closeDropdown = (element) => {
  if (!dropdown.value.contains(element.target)) {
    isDropdownVisible.value = false
  }
}

onMounted(() => {
  window.addEventListener('click', closeDropdown)
})

onBeforeUnmount(() => {
  window.addEventListener('click', closeDropdown)
})

</script>

<template>
  <div class="custom-select" :style="{width: width}" ref="dropdown">
    <button @click="isDropdownVisible = !isDropdownVisible"
            class="custom-select__button"
            role="combobox"
            aria-labelledby="select button"
            aria-haspopup="listbox"
            aria-expanded="false"
            aria-controls="select-dropdown">
      <span class="custom-select__selected-value" v-if="mappedSelectedOption"> {{ mappedSelectedOption }}</span>
      <span class="custom-select__placeholder" v-else>Выберите название региона</span>
      <span class="custom-select__arrow" :class="{'is-open' : isDropdownVisible}">
        <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M3 6L8 11L13 6" stroke="#BBC3FF" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </span>
    </button>
    <Transition name="fade">
      <ul class="custom-select__dropdown" role="listbox" id="select-dropdown" v-if="isDropdownVisible">
        <li class="custom-select__option" role="option" v-for="option in options" :key="option.id"
            @click="toggleOptionSelect(option)">
          <input class="custom-select__input" type="radio" :id="option.id" name="options"
                 :checked="option === selectedOption"/>
          <label class="custom-select__label" :class="{'is-checked': option === selectedOption}" :for="option.title">{{ option.title || option }}
            <Transition name="fade">
                <svg v-if="option === selectedOption" xmlns="http://www.w3.org/2000/svg"  viewBox="0 0 24 24" width="24px" height="24px"><path d="M 19.980469 5.9902344 A 1.0001 1.0001 0 0 0 19.292969 6.2929688 L 9 16.585938 L 5.7070312 13.292969 A 1.0001 1.0001 0 1 0 4.2929688 14.707031 L 8.2929688 18.707031 A 1.0001 1.0001 0 0 0 9.7070312 18.707031 L 20.707031 7.7070312 A 1.0001 1.0001 0 0 0 19.980469 5.9902344 z"/></svg>
            </Transition>
          </label>
        </li>
      </ul>
    </Transition>
  </div>
</template>

<style scoped lang="scss">
.custom-select {
  position: relative;
  max-width: 100%;
  color: #000;

  &__button {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    padding: 10px 16px;
    border-radius: 7px;
    border: 1px solid #F968bf;
    background: #FFF;
    cursor: pointer;
    outline: none;
    transition: border-color 0.3s ease-in-out;
  }

  &__selected-value {
    text-align: left;
    color: #29277d;
  }

  &__arrow {
    transition: transform ease-in-out 0.3s;

    &.is-open {
      transform: rotate(180deg);
    }
  }

  &__dropdown {
    position: absolute;
    list-style: none;
    width: 100%;
    background-color: #fff;
    border: 1px solid #F968bf;
    border-radius: 7px;
    padding: 10px 0;
    margin-top: 2px;
    max-height: 152px;
    overflow-y: auto;
    transition: 0.5s ease;
    z-index: 1;

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

  &__option {
    position: relative;
    cursor: pointer;
    display: flex;
    align-items: center;
    transition: background-color .3s ease-in-out;

    &:hover {
      background-color: #DADEFE;
    }
  }

  &__label {
    width: 100%;
    padding: 8px 16px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: space-between;
    color: #29277d;
    font-size: 16px;
    font-style: normal;
    font-weight: 400;
    line-height: 24px;

    &.is-checked {
      background-color: rgba(218, 222, 254, 0.2);
    }
  }

  &__input {
    position: absolute;
    left: 0;
    opacity: 0;
  }

  &__placeholder {
    color: rgba(41, 39, 125, 0.40);
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
