<template>
  <div class="container mx-auto">
    <Dropdown :items="dropdownItems" />
  </div>
</template>

<script>
import Dropdown from '../components/Dropdown.vue';

export default {
  components: {
    Dropdown,
  },
  data() {
    return {
      dropdownItems: [
        { title: 'Option 1', value: 'option1' },
        { title: 'Option 2', value: 'option2' },
        { title: 'Option 3', value: 'option3' },
      ],
    };
  },
};
</script>
