<template>
  <div class="list-wrapper">
    <AppSearch @update:search="updateSearch" />
    <ListOfGames
      :listOfGames="listOfGames"
      :search="search"
      :activeGameName="activeGameName"
      @update:activeGame="updateActiveGame"
    />
  </div>
</template>

<script>
import AppSearch from "./AppSearch";
import ListOfGames from "./Lists/ListOfGames";

export default {
  props: {
    listOfGames: Array,
    activeGameName: String,
  },
  data() {
    return {
      search: "",
    };
  },
  methods: {
    updateSearch(value) {
      this.search = value;
    },
    updateActiveGame(id, name) {
      this.$emit("update:activeGame", id, name);
    },
  },
  components: {
    AppSearch,
    ListOfGames,
  },
};
</script>

<style>
.list-wrapper {
  background-color: white;
  border-radius: 5px;
  width: max-content;
  display: flex;
  flex-direction: column;
}
@media screen and (max-width: 1195px) {
  .list-wrapper {
    margin: 10px;
  }
}
</style>
