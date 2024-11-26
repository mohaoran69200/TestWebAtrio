<template>
  <div>
    <h2>Rechercher par entreprise</h2>
    <input v-model="company" placeholder="Nom de l'entreprise" />
    <button @click="searchByCompany">Rechercher</button>

    <ul v-if="peopleByCompany.length > 0">
      <li v-for="person in peopleByCompany" :key="person.id">
        {{ person.firstName }} {{ person.lastName }}
      </li>
    </ul>

    <p v-else>Aucune personne trouvée.</p>
  </div>
</template>

<script>
import apiClient from '../api.js';

export default {
  data() {
    return {
      company: '',
      peopleByCompany: [],
    };
  },
  methods: {
    async searchByCompany() {
      if (this.company) {
        try {
          const response = await apiClient.get(`/people/jobs/company/${this.company}`);
          this.peopleByCompany = response.data;
        } catch (e) {
          console.error('Erreur lors de la recherche', e);
        }
      }
    },
  },
};
</script>
