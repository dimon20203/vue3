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
          <ShowComponent v-if="editPersonId !== person.id" :person="person" @change-edit-person="changeEditPersonId" @delete-person="deletePerson" />
          <EditComponent v-else :person="person" @person-updated="updatePersonList" />
        </template>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';
import ShowComponent from './ShowComponent.vue';
import EditComponent from './EditComponent.vue';

export default {
  name: 'IndexComponent',
  components: {
    ShowComponent,
    EditComponent,
  },
  data() {
    return {
      people: null,
      editPersonId: null,
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
    changeEditPersonId(person) {
      this.editPersonId = person.id;
    },
    updatePersonList() {
      this.getPeople(); // Update person list after successful update
      this.editPersonId = null; // Reset edit person ID
    },
    deletePerson(personId) {
      axios.delete(`/api/people/${personId}`)
        .then(() => {
          this.getPeople(); // Update person list after successful delete
        })
        .catch(error => {
          console.error(error);
        });
    },
  },
};
</script>

<style>
/* Ваши стилі тут */
</style>
