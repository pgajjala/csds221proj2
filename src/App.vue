<template>
  <ToDo> <AddPopup /> <EditPopup /></ToDo>
</template>

<script>
import ToDo from './components/ToDo.vue';
import AddPopup from './components/AddPopup.vue';
import EditPopup from './components/EditPopup.vue';

export default {
  name: 'App',
  components: {
    ToDo,
    AddPopup,
    EditPopup,
  },
};
</script>
