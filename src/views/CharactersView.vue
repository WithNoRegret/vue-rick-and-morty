<template>
    <div>
      <div v-if="isLoading">Loading...</div>
      <main v-else class="charactersView">
        <FiltersComponent @search="handleFilter" />
        <CharacterPagination v-if="cards.length" :totalPages="totalPages" :currentPage="page" @page-changed="handlePagination" />
        <CharacterCardList v-if="cards.length" :cards="cards" />
        <CharacterPagination v-if="cards.length" :totalPages="totalPages" :currentPage="page" @page-changed="handlePagination" />
        <div v-else class="no-results"> Sorry, No characters found :( </div>
      </main>
    </div>
  </template>
  
  <script>
  import CharacterCardList from '../components/CharacterCardList.vue';
  import FiltersComponent from '../components/FiltersComponent.vue';
  import CharacterPagination from '../components/CharacterPagination.vue';
  import { fetchCharacters } from '../helpers/fetchApi';
  
  export default {
    name: 'App',
    components: {
      CharacterCardList,
      FiltersComponent,
      CharacterPagination
    },
    data() {
      return {
        cards: [],
        name: '',
        status: '',
        page: 0,
        totalPages: 0,
        isLoading: true
      };
    },
    async mounted() {
      try {
        const data = await fetchCharacters();
        this.page = 1;
        this.cards = data.results;
        this.totalPages = data.info.pages;
        this.isLoading = false;
      } catch (error) {
        console.error(error.message);
        this.cards = [];
        this.page = 0;
        this.totalPages = 0;
        this.isLoading = false;
      }
    },
    methods: {
      async handleFilter(filters) {
        this.name = filters.name;
        this.status = filters.status;
        this.page = 1;
        try {
          const data = await fetchCharacters(this.name, this.status, this.page);
          if (!data.results.length) {
            this.page = 0;
            this.totalPages = 0;
            this.cards = [];
          }
          this.cards = data.results;
          this.totalPages = data.info.pages;
          this.isLoading = false;
        } catch (error) {
          console.error(error.message);
          this.cards = [];
          this.page = 0;
          this.totalPages = 0;
          this.isLoading = false;
        }
      },
      async handlePagination(page) {
        this.page = page;
        try {
          const data = await fetchCharacters(this.name, this.status, this.page);
          if (!data.results.length) {
            this.page = 0;
            this.totalPages = 0;
            this.cards = [];
            this.isLoading = false;
          }
          this.cards = data.results;
          this.totalPages = data.info.pages;
          this.isLoading = false;
        } catch (error) {
          console.error(error.message);
          this.cards = [];
          this.page = 0;
          this.totalPages = 0;
          this.isLoading = false;
        }
      }
    }
  };
  </script>
  
  <style>
.charactersView {
    display: flex;
    align-items: stretch;
    flex-direction: column;
    gap: 20px;
}

.no-results {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
  </style>