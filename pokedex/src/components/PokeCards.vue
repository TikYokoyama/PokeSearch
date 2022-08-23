<template>
  <main>
    <div>
      <input v-model="search" type="text" placeholder="Search" />
      <!-- {{ search }} -->
    </div>
    <hr />
    <div class="cards-container">
      <div class="card" v-for="pokemon in filtered_pokemons" :key="pokemon.name">
        <div class="card-content">
          <img
            class="card-image"
            :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${get_id(
              pokemon
            )}.png`"
            :alt="pokemon.name"
          />
          <div class="card-text">
            <h2 class="card-name">{{ get_name(pokemon) }}</h2>
            <p><strong>#</strong>{{ get_id(pokemon) }}</p>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import axios from "axios";
export default {
  name: "PokeCards",

  data() {
    return {
      pokemons: [],
      search: "",
    };
  },
  mounted() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151").then((response) => {
      this.pokemons = response.data.results;
    });
  },
  methods: {
    get_id(pokemon) {
      return Number(pokemon.url.split("/")[6]);
    },
    get_name(pokemon) {
      return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1);
    },
  },
  computed: {
    filtered_pokemons() {
      return this.pokemons.filter((item) => {
        return item.name.includes(this.search);
      });
    },
  },
};
</script>

<style scoped>
input {
  font-size: 25px;
  width: 100%;
  margin: 0 100px;
  border: none;
  background-color: #66c5ed;
}

.card {
  border-radius: 5px;
  background-color: #fcd26f;
  margin: 5px;
}

.cards-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
}
.card-content {
  width: 150px;
  border: 1px solid;
  border-color: #f0a10e;
  box-shadow: 1px 1px #ff2a1f;
  border-radius: 5px;
  text-align: center;
  padding: 0 50px;
}

.card-image {
  width: 100%;
}

.card-name {
  margin: 0;
}

.card-text {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}
</style>
