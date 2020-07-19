<template>
  <input
    type="text"
    class="list__search"
    placeholder="Поиск..."
    @input="updateSearch($event)"
  />
</template>

<script>
export default {
  methods: {
    updateSearch(e) {
      this.$emit('update:search', e.target.value);
    }
  }
}
</script>

<style>
.list__search {
  margin: 10px 10px 0;
  padding: 8px 10px;
  font-family: inherit;
  font-size: 16px;
}
</style>
