<template>
  <div class="list-achieve-wrapper" v-if="achievements.length">
    <h2 class="list-achieve__header">{{ header }}</h2>
    <ul class="list-of-achievements">
      <ItemAchievement
        v-for="achieve in achievements"
        :key="achieve.name"
        :achieve="achieve"
        :gameName="gameName"
      />
    </ul>
  </div>
</template>

<script>
import ItemAchievement from "@/components/ListItems/ItemAchievement";

export default {
  props: {
    achievements: Array,
    header: String,
    gameName: String
  },
  components: {
    ItemAchievement,
  },
};
</script>

<style>
.list-achieve-wrapper {
  background-color: #1b2838;
  padding: 10px;
  align-self: flex-start
}
.list-achieve-wrapper:not(:first-child) {
  margin-left: 20px;
}
.list-achieve__header {
  color: white;
  margin: 0;
}
.list-of-achievements {
  padding: 0; 
  list-style: none;
}

@media screen and (max-width: 815px) {
  .list-achieve-wrapper {
    margin: 10px auto 0;
    width: calc(100% - 20px);
  }
  .list-achieve-wrapper:not(:first-child) {
    margin-left: auto;
  }
}
</style>
