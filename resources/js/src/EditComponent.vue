<template>
  <tr>
    <th scope="row">{{ person.id }}</th>
    <td><input v-model="editedName" type="text" class="form-control"></td>
    <td><input v-model="editedAge" type="number" class="form-control"></td>
    <td><input v-model="editedJob" type="text" class="form-control"></td>
    <td>
      <a class="btn btn-success" @click.prevent="updatePerson" href="javascript:void(0)">Update</a>
    </td>
  </tr>
</template>

<script>
import axios from 'axios';

export default {
  name: 'EditComponent',
  props: {
    person: Object,
  },
  data() {
    return {
      editedName: this.person.name,
      editedAge: this.person.age,
      editedJob: this.person.job,
    };
  },
  methods: {
    updatePerson() {
      axios.put(`/api/people/${this.person.id}`, {
        name: this.editedName,
        age: this.editedAge,
        job: this.editedJob,
      })
        .then(() => {
          // Emit event to notify parent component
          this.$emit('person-updated');
        })
        .catch(error => {
          console.error(error);
        });
    },
  },
};
</script>

<style>
/* Ваші стилі тут */
</style>
