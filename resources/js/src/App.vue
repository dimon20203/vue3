<template>
  <div>
    <CreateComponent></CreateComponent>
    <IndexComponent  ref="index"></IndexComponent>
  </div>
</template>

<script>
import CreateComponent from './CreateComponent.vue';
import IndexComponent from './IndexComponent.vue';

export default {
  name: 'App',
  components: {
    CreateComponent,
    IndexComponent,
  },
  data() {
    return {};
  },
  mounted() {
    // Ваш код, який викликається після монтування компонента
  },
  methods: {
    parentLog() {
      //console.log('Parent log from IndexComponent');
    },
  },
  computed: {
    // Ваші обчислені властивості
  },
};
</script>

<style scoped>
/* ваші стилі тут */
</style>
