<template>
  <div>
    <h2>Ajouter un emploi</h2>
    <form @submit.prevent="addJob">
      <div>
        <label for="company">Entreprise:</label>
        <input v-model="newJob.company" type="text" id="company" required />
      </div>
      <div>
        <label for="position">Poste:</label>
        <input v-model="newJob.position" type="text" id="position" required />
      </div>
      <div>
        <label for="startDate">Date de début:</label>
        <input v-model="newJob.startDate" type="date" id="startDate" required />
      </div>
      <div>
        <label for="endDate">Date de fin:</label>
        <input v-model="newJob.endDate" type="date" id="endDate" />
      </div>
      <button type="submit">Ajouter emploi</button>
    </form>
  </div>
</template>

<script>
import apiClient from '../api.js';

export default {
  props: ['personId'],
  data() {
    return {
      newJob: {
        company: '',
        position: '',
        startDate: '',
        endDate: ''
      },
    };
  },
  methods: {
    async addJob() {
      try {
        const response = await apiClient.post(`/people/${this.personId}/jobs`, this.newJob);
        console.log('Emploi ajouté', response.data);
      } catch (e) {
        console.error('Erreur lors de l\'ajout de l\'emploi', e);
      }
    },
  },
};
</script>
