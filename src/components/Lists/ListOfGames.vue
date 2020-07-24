<template>
  <ul class="list-of-games">
    <ItemGame
      v-for="game in editedList"
      :key="game.appid"
      :name="game.name"
      :id="game.appid"
      :activeGameName="activeGameName"
      @update:activeGame="updateActiveGame"
    />
  </ul>
</template>

<script>
import ItemGame from "@/components/ListItems/ItemGame";

export default {
  props: {
    listOfGames: Array,
    search: String,
    activeGameName: String
  },
  computed: {
    editedList() {
      return this.listOfGames
        .filter((game) => {
          return (
            game.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1
          );
        })
        .sort((a, b) => {
          return a.name.localeCompare(b.name);
        });
    },
  },
  methods: {
    updateActiveGame(id, name) {
      this.$emit("update:activeGame", id, name);
    },
  },
  components: {
    ItemGame,
  },
};
</script>

<style>
.list-of-games {
  list-style: none;
  padding: 0;
}
@media screen and (max-width: 1195px) {
  .list-of-games {
    display: flex;
    flex-wrap: wrap;
    max-width: calc(100vw - 37px);
    max-height: 450px;
    overflow: auto;
  }
}
</style>
