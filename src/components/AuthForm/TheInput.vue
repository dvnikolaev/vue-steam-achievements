<template>
  <label class="input">
    <span class="input__label">{{ label }}</span>
    <input type="text" class="input__input" required @input="changeValue($event)"/>
    <a :href="link" class="input__hint" target="_blank">{{ hint }}</a>
  </label>
</template>

<script>
export default {
  props: {
    type: String
  },
  computed: {
    label() {
      switch(this.type) {
        case 'apiKey':
          return 'Ваш STEAM API KEY';
        case 'steamId':
          return 'Ваш STEAM ID';
        default:
          return '';
      }
    },
    hint() {
      switch(this.type){
        case 'apiKey':
          return 'Узнать свой STEAM API KEY';
        case 'steamId':
          return 'Узнать свой STEAM ID';
        default:
          return '';
      }
    },
    link() {
      switch(this.type) {
        case 'apiKey':
          return 'https://steamcommunity.com/login/home/?goto=%2Fdev%2Fapikey'
        case 'steamId':
          return 'https://www.youtube.com/watch?v=1T18wZgvwPw'
        default:
          return '';
      }
    }
  },
  methods: {
    changeValue(e) {
      this.$emit('update:input',e.target.value,this.type);
    }
  }
}
</script>

<style>
.input {
  display: flex;
  flex-direction: column;
  margin-top: 10px;
}
.input__label {
  text-transform: uppercase;
  font-weight: bold;
}
.input__input {
  padding: 10px;
  margin-top: 5px;
  border: 1px solid rgb(90,90,90);
}
.input__input:focus {
  outline: none;
  border-color: black;
}
.input__hint {
  font-size: 13px;
  color: blue;
  align-self: flex-end;
}
</style>
