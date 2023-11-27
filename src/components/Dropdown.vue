<template>
  <div class="relative inline-block text-left w-56 mt-12">
    <!-- Dropdown Trigger -->
    <button
        type="button"
        class="inline-flex justify-center w-full rounded-md border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 focus:outline-none focus:border-blue-300"
        @click="toggleDropdown"
    >
      Select
     <icon-arrow-down></icon-arrow-down>
    </button>

    <!-- Dropdown Content -->
    <transition name="fade">
      <div v-if="isOpen" class="origin-top-right absolute left-0 mt-2 w-56 rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5 focus:outline-none">
        <div class="py-1" role="menu" aria-orientation="vertical" aria-labelledby="options-menu">
          <!-- Dropdown Items -->
          <div
              v-for="(item, index) in items"
              :key="index"
              @click="toggleSelection(item)"
              :class="{ 'bg-gray-100': isSelected(item) }"
              class="block px-4 py-2 text-sm text-gray-700 cursor-pointer hover:bg-gray-100"
          >
            {{ item.title }}
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import { ref } from 'vue';
import IconArrowDown from "./icons/IconArrowDown.vue";

export default {
  components: {IconArrowDown},
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
  setup(props) {
    const isOpen = ref(false);
    const selectedItems = ref([]);

    const toggleDropdown = () => {
      isOpen.value = !isOpen.value;
    };

    const toggleSelection = (item) => {
      const index = selectedItems.value.findIndex((selectedItem) => selectedItem.value === item.value);

      if (index !== -1) {
        selectedItems.value.splice(index, 1);
      } else {
        selectedItems.value.push(item);
      }
    };

    const isSelected = (item) => {
      return selectedItems.value.some((selectedItem) => selectedItem.value === item.value);
    };

    return {
      isOpen,
      selectedItems,
      toggleDropdown,
      toggleSelection,
      isSelected,
    };
  },
};
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
