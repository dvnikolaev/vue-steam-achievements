<template>
  <form class="form">
    <h2>Форма</h2>
    <TheInput :type="'apiKey'" @update:input="updateInputValue" />
    <TheInput :type="'steamId'" @update:input="updateInputValue" />
    <TheButton @downloadGames="downloadGames" />
    <p>
      Важно! Ваш аккаунт должен быть открыт для всех!
      <a
        href="https://support.steampowered.com/kb_article.php?ref=4113-YUDH-6401&l=russian"
        target="_blank"
      >
        Как это сделать?
      </a>
    </p>
    <p class="form__error">{{ err }}</p>
  </form>
</template>

<script>
import TheInput from "./TheInput";
import TheButton from "./TheButton";

export default {
  props: {
    err: '',
  },
  methods: {
    updateInputValue(value, key) {
      this.$emit("update:inputValue", value, key);
    },
    async downloadGames() {
      this.$emit("update:listOfGames");
    },
  },
  components: {
    TheInput,
    TheButton,
  },
};
</script>

<style>
.form {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: white;
  min-width: 250px;
  padding: 20px;
}
.form__error {
  margin: 10px 0 0;
  font-size: 13px;
  color: red;
}
</style>
