<template>
  <div>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">id</th>
          <th scope="col">name</th>
          <th scope="col">age</th>
          <th scope="col">job</th>
          <th scope="col">edit</th>
          <th scope="col">delete</th>
        </tr>
      </thead>
      <tbody>
        <template v-for="person in people" :key="person.id">
          <tr v-if="editPersonId !== person.id">
            <th scope="row">{{ person.id }}</th>
            <td>{{ person.name }}</td>
            <td>{{ person.age }}</td>
            <td>{{ person.job }}</td>
            <td>
              <a class="btn btn-success" @click.prevent="changeEditPersonId(person.id, person.name, person.age, person.job)" href="javascript:void(0)">edit</a>
            </td>
            <td v-if="updatePerson">
              <a class="btn btn-danger" @click.prevent="deletePerson(person.id)" href="javascript:void(0)">delete</a>
            </td>
          </tr>
          <tr v-else>
            <th scope="row">{{ person.id }}</th>
            <td><input v-model="name" type="text" class="form-control"></td>
            <td><input v-model="age" type="number" class="form-control"></td>
            <td><input v-model="job" type="text" class="form-control"></td>
            <td>
              <a class="btn btn-success" @click.prevent="updatePerson(person.id)" href="javascript:void(0)">update</a>
            </td>
          </tr>
        </template>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'IndexComponent',
  data() {
    return {
      people: null,
      editPersonId: null,
      name: null,
      age: null,
      job: null
    };
  },
  mounted() {
    this.getPeople();

  },
  methods: {
    getPeople() {
      axios.get('/api/people')
        .then(res => {
          this.people = res.data;
        })
        .catch(error => {
          console.error(error);
        });
    },
    changeEditPersonId(id, name, age, job) {
      this.editPersonId = id;
      this.name = name;
      this.age = age;
      this.job = job;
    },
    updatePerson(id) {
      this.editPersonId = null;
      axios.put(`/api/people/${id}`, { name: this.name, age: this.age, job: this.job })
        .then(() => {
          this.getPeople(); // Обновление списка после успешного обновления на сервере
        })
        .catch(error => {
          console.error(error);
        });
    },
    deletePerson(id) {
      axios.delete(`/api/people/${id}`)
        .then(() => {
          this.getPeople(); // Обновление списка после успешного обновления на сервере
        })
        .catch(error => {
          console.error(error);
        });
    },
    indexLog() {

    },

  }
};
</script>

<style>
/* ваши стили здесь */
</style>