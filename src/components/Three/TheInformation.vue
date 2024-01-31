<template>
  <div>
    <!-- <div class="delete">
        <label class="inFont">DELETE</label>
        <label class="inNum">
          {{ deleteTime }}</label>
      </div> -->
    <div class="control_grid">
      <game-mode @set-mode="setGameMode"></game-mode>
    </div>

    <!-- <audio :src="recordMusicSrc" hidden preload="auto" ref="recordMus"></audio>
    <Transition name="fade">
      <div v-if="showRecord" class="successLayer">
        <img class="succeddImg" src="../../assets/2048/medal.png" />
      </div>
    </Transition> -->
    <game-modeUI></game-modeUI>
  </div>
</template>

<script>
import GameMode from './GameMode.vue';
import GameModeUI from './GameModeUI.vue';
export default {
  emits: ['newGame', 'changeGameMode'],
  inject: ['darkMode', 'gameMode'],
  components: {
    GameMode,
    GameModeUI,
  },
  data() {
    return {
      showRecord: false,
      hasShowed: false,
      recordMusicSrc: require("../../assets/2048/record.mp3"),
    }
  },
  methods: {
    setNewGame() {
      this.hasShowed = false;
      this.showQuickScore = [];
      this.$emit('newGame');
    },
    setGameMode(mode, interval) {
      this.setNewGame();
      this.$emit('changeGameMode', mode, interval);
    },
  },
  created() {
    let bestScore = localStorage.getItem('best');
    if (bestScore === null) {
      this.best = 0;
    } else {
      this.best = parseInt(bestScore);
    }
  },
}
</script>
<style scoped>
div {
  text-align: center;
  font-size: 19px;
  font-weight: 800;
}

label {
  display: block;
}

.show_grid,
.control_grid {
  position: fixed;
  display: grid;
  row-gap: 12px;
  column-gap: 12px;
  margin-bottom: 12px;
  justify-content: center;
  transition: 200ms left ease-out, 200ms top ease-out;
}

.control_grid {
  left: calc(75% + 30px);
  top: calc(50% + 6px);
  grid-template: "new" 62px/100px;
  /* 设置成62px而不是50px 是因为要给gameMode添加间隙 */
}

/* 该项在TheBackground.vue也有修改 */
@media screen and (max-width: 1100px) {

  .control_grid {
    position: fixed;
    left: calc(50% - 106px);
    top: 89%;
  }
}

@media screen and (max-width: 800px) {
  .control_grid {
    position: fixed;
    left: calc(50% - 162px);
    top: 89%;
  }
}

.inFont {
  font-size: 14px;
  color: #ede0c8;
  line-height: 40px;
}

.inNum {
  font-size: 20px;
  color: white;
  line-height: 5px;
}

.successLayer {
  z-index: 888;
  position: fixed;
  display: flex;
  justify-content: center;
  align-items: center;
  left: 45%;
  top: 40%;
  width: 10%;
  height: 20%;
}

.succeddImg {
  width: 120px;
}

.fade-leave-to,
.fade-enter-from {
  opacity: 0;
  transform: translateX(100px);
}

.fade-leave-from,
.fade-enter-to {
  opacity: 1;
}

.fade-leave-active,
.fade-enter-active {
  transition: all 0.6s ease-in-out;
}
</style>