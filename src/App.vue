<template>
  <ToDo> <AddPopup /> </ToDo>
</template>

<script>
import ToDo from './components/ToDo.vue';
import AddPopup from './components/AddPopup.vue';

export default {
  name: 'App',
  components: {
    ToDo,
    AddPopup,
  },
};
</script>
