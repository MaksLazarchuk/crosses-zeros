<template>
  <div id="app">
    <div class="people">
      <div class="player1 player">
        <h2>Ім'я гравця</h2>
        <input class="text" v-model="players[0]" type="text" />
      </div>
      <div class="player2 player">
        <h2>Ім'я гравця</h2>
        <input class="text" v-model="players[1]" type="text" />
      </div>
      <div class="player-active player" v-if="!isGameOver">
        <h2>Ходить</h2>
        <input
          class="text"
          disabled
          :value="players[activePlayer]"
          type="text"
        />
      </div>
      <div class="player-active player">
        <button class="restart" @click="restart">&#8634;</button>
      </div>
    </div>
    <div id="background">
      <div class="line horizontally-top" />
      <div class="line horizontally-bottom" />
      <div class="line vertically-left" />
      <div class="line vertically-right" />

      <div class="cell-box">
        <div
          v-for="cell in 9"
          :key="cell"
          class="cell"
          @click="move(cell)"
          :class="{ [`cell${cell}`]: true, active: moves.includes(cell) }"
        >
          <template v-if="moves.includes(cell)">
            <Cross v-if="moves.indexOf(cell) % 2 === 0" />
            <Zero v-else />
          </template>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Cross from "./components/Cross.vue";
import Zero from "./components/Zero.vue";

const winCombination = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],

  [1, 4, 7],
  [2, 5, 8],
  [3, 6, 9],

  [1, 5, 9],
  [3, 5, 7],
];

export default {
  components: { Cross, Zero },
  data() {
    return {
      players: ["Nazar", "Max"],

      moves: [],

      isGameOver: false,
    };
  },

  methods: {
    move(value) {
      if (this.isGameOver) return;
      if (this.moves.includes(value)) return;

      this.moves.push(value);

      this.checkWinOrDraw();
    },

    checkWinOrDraw() {
      if (this.moves.length < 5) return;

      // перевіряємо хто ходив в останній раз
      const playerIndex = this.moves.length % 2 === 0 ? 1 : 0;

      // фільтрую всі ходи, які зробив гравець (через один)
      const playerMoves = this.moves.filter(
        (value, i) => i % 2 === playerIndex
      );

      // виграш буде true, якщо є хоч одна комбінація з масиву winCombination
      const isWin = winCombination.some(
        // така, що кожен її хід
        (compination) =>
          compination.every(
            // співпадає з ходом гравця
            (move) => playerMoves.includes(move)
          )
      );

      if (isWin) {
        this.isGameOver = true;
        this.$toasted.show(
          `Гра зацінчилася. Виграв гравець ${this.players[playerIndex]}`,
          {
            theme: "outline",
            position: "bottom-right",
            duration: 5000,
            className: "myToast",
          }
        );
        return;
      }

      if (this.moves.length === 9) {
        this.isGameOver = true;
        this.$toasted.show("Нічия. Кінець гри!", {
          theme: "outline",
          position: "bottom-right",
          duration: 5000,
          className: "myToast",
        });
      }
    },

    restart() {
      this.moves = [];
      this.isGameOver = false;

      this.players.reverse();
    },
  },

  computed: {
    activePlayer() {
      return this.moves.length % 2;
    },
  },
};
</script>

<style>
body {
  padding: 0;
  margin: 0;
  background-color: rgb(43, 43, 43);
}
#app {
  width: 100%;
}
.people {
  position: relative;
  display: flex;
  width: max-content;
  margin-left: auto;
  margin-right: auto;
  color: white;
}
.player {
  margin-right: 25px;
  margin-left: 25px;
}
h2 {
  font-size: 28px;
  text-align: center;
}
.text {
  height: 40px;
  background-color: rgb(43, 43, 43);
  width: 150px;
  color: white;
  font-size: 26px;
  border: none;
  font-weight: 400;
  text-align: center;
  margin-top: -10px;
}
#background {
  height: 600px;
  width: 600px;
  margin-top: 100px;
  margin-left: auto;
  margin-right: auto;
  border-radius: 6px;
}
.line {
  position: absolute;
  background-color: white;
}
.horizontally-top {
  width: 600px;
  height: 8px;
  margin-top: 196px;
}
.horizontally-bottom {
  width: 600px;
  height: 8px;
  margin-top: 396px;
}
.vertically-left {
  height: 601px;
  width: 8px;
  margin-left: 196px;
}
.vertically-right {
  height: 601px;
  width: 8px;
  margin-left: 396px;
}
.cell-box {
  display: flex;
  flex-wrap: wrap;
}
.cell {
  height: 200px;
  width: 200px;
  cursor: pointer;
  transition: background-color 0.2s ease-in-out;
}
.cell:hover {
  background: rgba(0, 0, 250, 0.5);
}
.cell.active {
  pointer-events: none;
}

.restart {
  width: 50px;
  height: 50px;
  font-size: 30px;
  background: rgba(0, 0, 250, 0.5);
  color: white;
  border: 0;
  border-radius: 5px;
  margin-top: 40px;
}
.myToast {
  font-size: 32px !important;
}
</style>
