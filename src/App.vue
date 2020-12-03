<template>
  <div id="app">
    <div class="people">
      <div class="player1 player">
        <h2>Ім'я гравця</h2>
        <input class="text" v-model="player1" type="text" />
      </div>
      <div class="player2 player">
        <h2>Ім'я гравця</h2>
        <input class="text" v-model="player2" type="text" />
      </div>
    </div>
    <div id="background">
      <div class="line horizontally-top" />
      <div class="line horizontally-bottom" />
      <div class="line vertically-left" />
      <div class="line vertically-right" />
      <div class="cell-box">
        <div class="cell cell1">
          <div class="crosses">
            <div class="line-cross line1-crosses" />
            <div class="line-cross line2-crosses" />
          </div>
        </div>
        <div class="cell cell2">
          <div class="zeros" />
        </div>
        <div class="cell cell3"></div>
        <div class="cell cell4"></div>
        <div class="cell cell5"></div>
        <div class="cell cell6"></div>
        <div class="cell cell7"></div>
        <div class="cell cell8"></div>
        <div class="cell cell9"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      player1: "Nazar",
      player2: "Max",
    };
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
}
.line-cross {
  background-color: white;
  height: 175px;
  width: 30px;
  border-radius: 20px;
  margin: 12.5px;
}
.crosses {
  height: 200px;
  position: absolute;
  width: 200px;
}
.line1-crosses {
  margin-left: 85px;
  transform: rotate(-45deg);
}
.line2-crosses {
  margin-left: 85px;
  margin-top: -187px;
  transform: rotate(45deg);
}
.zeros {
  width: 90px;
  height: 90px;
  position: absolute;
  border: solid 30px white;
  border-radius: 50%;
  margin: 25px;
}
</style>
