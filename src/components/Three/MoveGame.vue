<template>
  <div class="wrapper">
    <Transition name="fade">
      <div v-if="!gameOver" class="iconarea">
        <label :class="{ icon_dark: darkMode, icon_light: !darkMode }">Threes!</label>
      </div>
    </Transition>
    <div class="game">
      <the-background></the-background>
      <the-three @game-over="getGameOver" @trigger-show="clearNote" ref="coreRef"></the-three>

    </div>
    <div class="inf">
      <TheInformation ref="infRef" @change-game-mode="setNewGame">
      </TheInformation>
    </div>
    <game-over ref="gameOverRef"></game-over>
    <label class="version">最近更新: 2023年3月28日</label>
  </div>
</template>
<script>
import TheThree from './TheThree.vue';
// import CoreGame from './CoreGame.vue'
import TheInformation from './TheInformation.vue';
import TheBackground from './TheBackground.vue';
import GameOver from './GameOver.vue';
import { computed } from 'vue'
export default {
  inject: ['darkMode'],
  components: {
    TheInformation,
    TheThree,
    TheBackground,
    GameOver,
  },
  provide() {
    return {
      gameMode: computed(() => this.gameMode),
      interval: computed(() => this.interval),
      gameOver: computed(() => this.gameOver),
    }
  },
  data() {
    return {
      gameMode: 'custom', //custom or doubly or timer
      interval: 100,
      gameOver: false,
    }
  },
  methods: {
    setNewGame(mode, interval) {
      this.gameMode = mode;
      this.interval = interval;
      this.gameOver = false;
      this.$refs.gameOverRef.gameOver = false;
      this.$refs.coreRef.isSetNewGame = true;
    },
    getGameOver() {
      this.gameOver = true;
      // setTimeout(() => {
      //   this.$refs.gameOverRef.cells = cells;
      //   this.$refs.gameOverRef.maxNum = maxNum;
      this.$refs.gameOverRef.gameOver = true;
      // }, 1000);
    },
    clearNote() {
      this.$refs.gameOverRef.showNote = false;
    }
  },
  created() {
    let gameMode = localStorage.getItem('gameMode');
    let interval = localStorage.getItem('interval');
    if (gameMode === null) {
      this.gameMode = 'custom';
    } else {
      this.gameMode = gameMode;
    }
    if (interval === null) {
      this.interval = 1000;
    } else {
      this.interval = parseInt(interval);
    }
  },
}
</script>

<style scoped>
.iconarea>label {
  position: fixed;
  top: 60%;
  font-weight: 700;
  font-family: Cascadia Code;
}

.wrapper {
  position: fixed;
  left: 0px;
  top: 0px;
  width: 100%;
  height: 100%;
  display: flex;
  /* align-items: center;
  justify-content: center; */
}

/* 三列中:每一列width = 420px,其中game部分为 4*90 + 5*12 = 420px */

.iconarea {
  grid-area: icon;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: 200ms opacity ease-out;
}

/* 这一项在TheBackground.vue也有相应适配 */
@media screen and (max-width: 800px) {
  .iconarea {
    opacity: 0;
  }
}

.icon_light,
.icon_dark {
  position: fixed;
  left: calc(25% - 70px);
  top: 0%;
  width: 130px;
  height: 130px;
  color: white;
  font-size: 30px;
  line-height: 130px;
  border-radius: 20px;
}

.icon_light {
  /* background: linear-gradient(45deg, #00b7ff 0%, #ff0040 100%); */
  background-color: rgba(41, 41, 41, 0.285);
  /* border: linear-gradient(45deg, #00b7ff 0%, #ff0040 100%) solid 4px; */
  /* border: black solid 3px; */
  background-size: 400% 100%;
  color: #c9fbff;
  animation: gradient 7s infinite;
}

.icon_dark {
  /* background: linear-gradient(-45deg, #00ff9d, #ffb302); */
  background-color: rgba(100, 100, 100, 0.285);
  background-size: 400% 100%;
  color: #bdfce2;
  animation: gradient 7s infinite;
}

@keyframes gradient {
  0% {
    background-position: 0% 30%;
    color: #ffffff;
  }

  33% {
    background-position: 100% 50%;
    color: #ffbbbb;
  }

  66% {
    background-position: 50% 100%;
    color: #9df0ff;
  }

  100% {
    background-position: 0% 30%;
    color: #ffffff;
  }
}

.game {
  grid-area: game;
}

.inf {
  z-index: 40;
  grid-area: inf;
  display: flex;
  align-items: center;
  justify-content: center;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 1.5s;
}

.version {
  position: fixed;
  color: #00d9ff;
  top: 95%;
  left: 75%;
  width: 400px;
  font-family: NumberOnly;
}
</style>