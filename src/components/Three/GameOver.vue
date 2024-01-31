<template>
  <div>
    <Transition name="fade1">
      <div class="noMove" v-if="showNote">Can't Move！</div>
    </Transition>
    <Transition name="fade1">
      <div class="anyKey" v-if="showNote">Click Anywhere To Check</div>
    </Transition>

    <!-- <Transition name="slide">
      <div class="anykey" v-if="note2">单击查看分数</div>
    </Transition> -->
  </div>
  <!-- <div>{{ note1 }} {{ note2 }}</div> -->
</template>

<script>
export default {
  inject: ['darkMode'],
  data() {
    return {
      gameOver: false,
      showNote: false,
    }
  },
  watch: {
    gameOver(value) {
      if (value == true) {
        this.showNote = true;
        // this.disappear();
        // setTimeout(() => {
        //   this.note2 = true;
        // }, 2001)
        // setTimeout(() => {
        //   this.note2 = false;
        // }, 4000)
      } else {
        this.showNote = false;
      }
    }
  },
  methods: {
    disappear() {
      setTimeout(() => {
        this.note1 = false;
      }, 2000)
    }
  }
}
</script>

<style scoped>
.noMove,
.anyKey {
  position: fixed;
  top: 23%;
  left: 4%;
  z-index: 60;
  width: 320px;
  font-size: 32px;
  color: rgb(184, 10, 10);
}

.anyKey {
  /* top: 50%; */
  top: 31%;
  font-size: 30px;
  color: rgb(3, 172, 172);
}

@media screen and (max-width: 1100px) {
  h1 {
    top: calc(50% - 19.3px);
  }
}

.fade1-enter-from {
  opacity: 0;
  transform: translateY(-50px);
  /* transform: rotate(30deg); */
}

.fade1-enter-to {
  opacity: 1;
}

.fade1-leave-from {
  opacity: 1;
  transform: translateY(0px);
}

.fade1-leave-to {
  opacity: 0;
  transform: translateY(50px);
}

/* .fade-enter-to {
  opacity: 1;
  transform: translateY(0px);
}

.fade-leave-from {
  opacity: 1;
  transform: translateY(0px);
} */

.fade1-enter-active,
.fade1-leave-avtive {
  transition: all 600ms ease;
}
</style>