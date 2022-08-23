<template>
  <h1>PokeSearch</h1>
  <!-- <div>
    <input v-model="search" type="text" placeholder="Search" />
    {{ search }}
  </div> -->
  <PokeCards/>
</template>

<script>
import PokeCards from "./components/PokeCards.vue";

export default {
  name: "App",
  components: {
    PokeCards,
  },
  data() {
    return {
      search: "",
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

h1{
  text-align: center;
  font-size:50px;
}
</style>
