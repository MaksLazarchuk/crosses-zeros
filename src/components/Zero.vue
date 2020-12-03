<template>
  <div class="zeros" />
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
.zeros {
  width: 90px;
  height: 90px;
  position: absolute;
  border: solid 30px white;
  border-radius: 50%;
  margin: 25px;
  animation: example 0.5s;
}
</style>
