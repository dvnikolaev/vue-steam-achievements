<template>
  <li class="achievement">
    <a :href="linkString" class="achievement__link-search" target="_blank">
      <img :src="achieve.icon" alt="" class="achievement__icon" />
      <div class="achievement-text">
        <h5 class="achievement-text__title">{{ achieve.displayName }}</h5>
        <p class="achievement-text__description">{{ achieve.description }}</p>
      </div>
    </a>
  </li>
</template>

<script>
export default {
  props: {
    achieve: Object,
    gameName: String
  },
  computed: {
    linkString() {
      return `https://www.google.com/search?q=как+получить+достижение+${this.achieve.displayName.split(' ').join('+')}+${this.gameName}`
    }
  }
};
</script>

<style>
.achievement {
  transition: filter .2s ease;
}
.achievement:not(:first-child) {
  margin-top: 20px;
}
.achievement:hover {
  filter: opacity(0.5);
}
.achievement__link-search {
  display: flex;
  text-decoration: none;
}
.achievement-text {
  background-color: #080c11;
  margin-left: 5px;
  padding: 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  width: 90%;
  max-width: 450px;
}
.achievement-text__title {
  color: #e1e1e1;
  margin: 0;
}
.achievement-text__description {
  color: #898989;
  margin: 0;
  font-size: 14px;
}

@media screen and (max-width: 815px) {
  .achievement-text {
    max-width: none;
  }
}
</style>
