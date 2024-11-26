<template>
  <div>
    <h2>Rechercher emplois par date</h2>
    <label for="startDate">Date de début:</label>
    <input v-model="startDate" type="date" id="startDate" />

    <label for="endDate">Date de fin:</label>
    <input v-model="endDate" type="date" id="endDate" />

    <button @click="searchJobsByDate">Rechercher</button>

    <ul v-if="jobs.length > 0">
      <li v-for="job in jobs" :key="job.company">
        {{ job.position }} à {{ job.company }} du {{ job.startDate }} au {{ job.endDate }}
      </li>
    </ul>

    <p v-else>Aucun emploi trouvé pour cette période.</p>
  </div>
</template>

<script>
import apiClient from '../api.js';

export default {
  props: ['personId'],
  data() {
    return {
      startDate: '',
      endDate: '',
      jobs: [],
    };
  },
  methods: {
    async searchJobsByDate() {
      try {
        const response = await apiClient.get(`/people/${this.personId}/jobs`, {
          params: {
            startDate: this.startDate,
            endDate: this.endDate,
          },
        });
        this.jobs = response.data;
      } catch (e) {
        console.error('Erreur lors de la recherche des emplois', e);
      }
    },
  },
};
</script>
