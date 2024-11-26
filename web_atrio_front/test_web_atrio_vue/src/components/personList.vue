<template>
  <div>
    <h2>Liste des personnes</h2>
    <ul>
      <li v-for="person in peoples" :key="person.id">
        {{ person.firstName }} {{ person.lastName }} - {{ person.age }} ans
        <ul>
          <li v-for="(job, index) in person.currentJobs" :key="index">
            {{ job.position }} à {{ job.company }}
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
import apiClient from '../api.js';

export default {
  data() {
    return {
      peoples: [],
    };
  },
  async mounted() {
    try {
      const response = await apiClient.get('/people');
      this.peoples = response.data;
    } catch (e) {
      console.error('Erreur lors de la récupération des personnes', e);
    }
  },
};
</script>
