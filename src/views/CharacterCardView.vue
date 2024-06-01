<template>
    <div v-if="isLoading">Loading...</div>
    <div v-else>
        <div class="cardView">
            <h1>{{ card.name }}</h1>
            <img :src="card.image" :alt="card.name">
            <p>{{ card.status }} - {{ card.species }}</p>
            <p>Last known location: {{ card.location.name }}</p>
        </div>
        <RouterLink to="/" class="back-button">Back to character list</RouterLink>
    </div> 
</template>

<script>
import { fetchCharacter } from '../helpers/fetchApi';

export default {
    name: 'CharacterCardView',
    data() {
        return {
            card: {},
            isLoading: true
        }
    },
    async created() {
        const id = this.$route.params.id;
        const data = await fetchCharacter(id);
        this.card = data;
        this.isLoading = false;
    }
};
</script>

<style scoped>
.cardView {
    padding: 20px;

    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
}

.back-button {
    margin-block: 20px;
}

.back-button:before {
    content: "⬅️";
    margin-right: 5px;
}
</style>