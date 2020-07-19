<template>
  <button class="button" type="button" @click="download">Готово</button>
</template>


<script>
export default {
  methods: {
    download() {
      this.$emit('downloadGames');
    }
  }
}
</script>

<style>
.button {
  display: block;
  margin-left: auto;
  margin-top: 10px;
  border: none;
  background: CornflowerBlue;
  color: white;
  cursor: pointer;
  font-weight: bold;
  font-family: inherit;
  padding: 10px 20px;
}
.button:hover,
.button:focus {
  background: rgb(84, 124, 199);
}
</style>