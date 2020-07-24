<template>
  <transition name="slideY">
    <div class="notification" v-if="text">
      <p class="notification__message">{{ text }}</p>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    text: String
  },
};
</script>

<style>
.notification {
  position: fixed;
  left: 50%;
  top: 5%;
  transform: translateX(-50%);
  padding: 10px 20px;
  background-color: #d1ecf1;
  border-radius: 2px;
}
.notification__message {
  margin: 0;
  color: #0c5460;
  font-weight: bold;
}

.slideY-enter-active,
.slideY-leave-active {
  transition: all .5s ease;
}
.slideY-enter {
  transform: translate(-50%,-50%);
  opacity: 0;
}
.slideY-enter-to {
  transform: translate(-50%,0);
  opacity: 1;
}
.slideY-leave-to {
  opacity: 0;
}

@media screen and (max-width: 645px) {
  .notification__message {
    text-align: center;
  }
}
</style>
