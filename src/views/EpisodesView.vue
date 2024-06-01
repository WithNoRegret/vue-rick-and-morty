<template>
    <div v-if="isLoading">Loading...</div>
    <div v-else class="card-list">
        <div v-for="card in cards" :key="card">
            <h1>{{ card.name }}</h1>
            <p>{{ card.air_date }}</p>
            <p>{{ card.episode }}</p>
        </div>
    </div>
</template>

<script>
import { fetchEpisodes } from '../helpers/fetchApi';

export default {
    name: 'EpisodesView',
    data() {
        return {
            cards: [],
            isLoading: true
        };
    },
    async mounted() {
      try {
        const data = await fetchEpisodes();
        this.cards = data;
        this.isLoading = false;
      } catch (error) {
        console.error(error.message);
        this.cards = [];
        this.isLoading = false;
      }
    },
};
</script>

<style scoped>
.card-list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
    gap: 20px;
}
</style>