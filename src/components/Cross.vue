<template>
  <div class="crosses">
    <div class="line-cross line1-crosses" />
    <div class="line-cross line2-crosses" />
  </div>
</template>

<style>
@keyframes example {
  from {
    transform: scale(1.8);
  }
  95% {
    transform: scale(0.95);
  }
}
.crosses {
  height: 200px;
  position: absolute;
  width: 200px;
  animation: example 0.5s;
}
.line-cross {
  background-color: white;
  height: 175px;
  width: 30px;
  border-radius: 20px;
  margin: 12.5px;
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
</style>
