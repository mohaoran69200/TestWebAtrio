<template>
  <div>
    <h2>Ajouter une personne</h2>
    <form @submit.prevent="addPerson">
      <div>
        <label for="firstName">Prénom:</label>
        <input v-model="newPerson.firstName" type="text" id="firstName" required />
      </div>
      <div>
        <label for="lastName">Nom:</label>
        <input v-model="newPerson.lastName" type="text" id="lastName" required />
      </div>
      <div>
        <label for="birthDate">Date de naissance:</label>
        <input v-model="newPerson.birthDate" type="date" id="birthDate" required />
      </div>
      <button type="submit">Ajouter</button>
    </form>
    <p v-if="errorMessage">{{ errorMessage }}</p>
  </div>
</template>

<script>
import apiClient from '../api.js';

export default {
  data() {
    return {
      newPerson: {
        firstName: '',
        lastName: '',
        birthDate: '',
      },
      errorMessage: ''
    };
  },
  methods: {
    async addPerson() {
      try {
        const response = await apiClient.post('/people', this.newPerson);
        console.log('Personne ajoutée', response.data);
      } catch (e) {
        if (e.response && e.response.data && e.response.data.error) {
          this.errorMessage = e.response.data.error;
        }
      }
    },
  },
};
</script>
