<template>
  <div class="app">
    <h1 class="tip-title">Leave a tip?</h1>
    <div class="tips-grid">
      <Tip class="fifteen" tip="15%" />
      <Tip class="twenty" tip="20%" />
      <Tip class="twenty-five" tip="25%" />
      <Tip class="custom" tip="Custom" />
      <Tip
        ref="noTipRef"
        class="no-tip"
        tip="No Tip"
        @mouseover="handleNoTipClick"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const noTipRef = ref();

function handleNoTipClick() {
  noTipRef.value.$el.style.width = "calc(100% - 80px)";
  const maxX = window.innerWidth - noTipRef.value.$el.offsetWidth / 2;
  const maxY = window.innerHeight - noTipRef.value.$el.offsetHeight;
  const randomX = (Math.random() * 2 - 1) * maxX;
  const randomY = Math.random() * maxY;

  noTipRef.value.$el.style.position = "fixed";
  noTipRef.value.$el.style.left = `${randomX}px`;
  noTipRef.value.$el.style.top = `${randomY}px`;
}
</script>

<style>
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 40px;
  justify-content: center;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}
.tip-title {
  color: #717274;
}
.tips-grid {
  display: grid;
  grid-template-areas:
    "fifteen twenty twenty-five"
    "custom custom custom"
    "no-tip no-tip no-tip";
  grid-template-rows: 2fr 1fr 1fr;
  gap: 12px;
  row-gap: 12px;
  width: 100%;
  height: fit-content;
}
.fifteen {
  grid-area: fifteen;
}
.twenty {
  grid-area: twenty;
}
.twenty-five {
  grid-area: twenty-five;
}

.no-tip {
  grid-area: no-tip;
}
.custom {
  grid-area: custom;
}
h1 {
  font-family: "Arial", sans-serif;
  font-weight: 200;
}
</style>
