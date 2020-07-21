<template>
  <li
    class="list-of-games__item"
    :class="activeGameClass"
    @click="updateActiveGame"
  >
    {{ name }}
  </li>
</template>

<script>
export default {
  props: {
    name: String,
    id: Number,
    activeGameName: String,
  },
  computed: {
    activeGameClass() {
      return this.activeGameName.toLowerCase() === this.name.toLowerCase()
        ? "list-of-games__item--active"
        : "";
    },
  },
  methods: {
    updateActiveGame() {
      this.$emit("update:activeGame", this.id, this.name);
    },
  },
};
</script>

<style>
.list-of-games__item {
  font-size: 18px;
  color: black;
  padding: 10px;
  text-align: center;
  transition: all 0.1s ease;
}
.list-of-games__item:not(.list-of-games__item--active):hover {
  background-color: lightslategray;
  color: white;
  cursor: pointer;
}
.list-of-games__item:last-child:hover {
  border-bottom-left-radius: 5px;
  border-bottom-right-radius: 5px;
}
.list-of-games__item--active {
  background-color: rgb(95, 109, 122);
  color: white;
  cursor: pointer;
}
</style>
