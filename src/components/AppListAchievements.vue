<template>
  <div>
    <div class="app-lists-achievements" v-if="showLists">
      <h2 class="lists-achievements__header">{{ activeGame.name }}</h2>
      <div class="lists-achievements-wrapper">
        <ListOfAchievements
          :achievements="activeGame.achievements"
          :header="'Неоткрытые достижения:'"
          :gameName="activeGame.name"
        />
        <ListOfAchievements
          :achievements="activeGame.hiddenAchievements"
          :header="'Неоткрытые скрытые достижения:'"
          :gameName="activeGame.name"
        />
      </div>
    </div>
    <AppSpinner v-if="showSpinner"/>
  </div>
</template>

<script>
import ListOfGames from "./Lists/ListOfGames";
import ListOfAchievements from "./Lists/ListOfAchievements";
import AppSpinner from "./AppSpinner";

export default {
  props: {
    activeGame: Object,
  },
  computed: {
    showLists() {
      return (
        (this.activeGame.achievements.length ||
        this.activeGame.hiddenAchievements.length) &&
        !this.activeGame.loading
      );
    },
    showSpinner() {
      return this.activeGame.loading
    }
  },
  components: {
    ListOfGames,
    ListOfAchievements,
    AppSpinner,
  },
};
</script>

<style>
.app-lists-achievements {
  background: white;
  align-self: flex-start;
  padding: 10px;
  margin-left: 10px;
  border-radius: 5px;
}
.lists-achievements__header {
  text-align: center;
  font-size: 25px;
}
.lists-achievements-wrapper {
  display: flex;
  align-self: flex-start;
}
</style>
