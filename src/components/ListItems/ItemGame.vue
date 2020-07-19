<template>
  <li
    class="list-of-games__item"
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
  },
  methods: {
    updateActiveGame() {
      this.$emit('update:activeGame',this.id,this.name);
    }
  }
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
.list-of-games__item:hover {
  background-color: lightslategray;
  color: white;
  cursor: pointer;
}
.list-of-games__item:last-child:hover {
  border-bottom-left-radius: 5px;
  border-bottom-right-radius: 5px;
}
</style>
