<template>
  <div>
    <div class="w-25">
      <div class="form-group w-75 ms-5 mt-5">
        <label for="name">Name:</label>
        <input v-model="name" type="text" class="form-control" id="name" placeholder="name">
      </div>
      <div class="form-group w-75 ms-5">
        <label for="age">Age:</label>
        <input v-model="age" type="number" class="form-control" id="age" placeholder="age">
      </div>
      <div class="form-group w-75 ms-5">
        <label for="job">Job:</label>
        <input v-model="job" type="text" class="form-control" id="job" placeholder="job">
      </div>
      <div class="form-group w-75 ms-5 mt-3">
        <button @click.prevent="addUser" class="btn btn-primary">Add User</button>
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios';


export default {
  name: 'CreateComponent',
  data() {
    return {
      name: null,
      age: null,
      job: null,

    };
  },
  mounted() {

  },
  methods: {
    addUser() {
      axios.post('/api/people', { name: this.name, age: this.age, job: this.job })
        .then(res => {
          this.name = null;
          this.age = null;
          this.job = null;
          this.$parent.$refs.index.getPeople();
          console.log(res.data); // Виводимо відповідь в консоль
        });
    },
  },
  components: {

  },
};
</script>


