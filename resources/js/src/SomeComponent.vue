<template>
  <div>
    <div>color: {{ obj.color }}</div>
    <div>number: {{ obj.number > 10 ? 'more' : 'less or equal' }}</div>
    <div>published: {{ obj.published ? 'published' : 'not published' }}</div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'SomeComponent',

  props: ['obj'],

  mounted() {
    // Ваш код, який викликається після монтування компонента
  },

  methods: {
    // Ваші методи
  },
};
</script>

<style>
/* ваші стилі тут */
</style>
