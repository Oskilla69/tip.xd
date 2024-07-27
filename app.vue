<template>
  <div class="app">
    <h1 class="tip-title">Leave a tip?</h1>
    <div class="tips-grid">
      <Tip class="fifteen" :tip="`${fifteen}%`" @click="handleTipClick" />
      <Tip class="twenty" :tip="`${twenty}%`" @click="handleTipClick" />
      <Tip
        class="twenty-five"
        :tip="`${twentyFive}%`"
        @click="handleTipClick"
      />
      <Tip class="fourty" :tip="`${fourty}%`" @click="handleTipClick" />
      <!-- <Tip class="custom" tip="Custom" /> -->
      <Tip
        ref="noTipRef"
        class="no-tip"
        tip="No Tip"
        @mouseover="handleNoTipClick"
        @click="handleNoTipClick"
      />
    </div>
    <LoadingOverlay v-if="loading" />
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import LoadingOverlay from "./components/LoadingOverlay.vue";

const noTipRef = ref();
const fifteen = ref(15);
const twenty = ref(20);
const twentyFive = ref(25);
const fourty = ref(40);
const loading = ref(false);

function handleNoTipClick() {
  noTipRef.value.$el.style.width = "calc(100% - 80px)";
  const maxX = window.innerWidth - noTipRef.value.$el.offsetWidth / 2;
  const maxY = window.innerHeight - noTipRef.value.$el.offsetHeight;
  const randomX = (Math.random() * 2 - 1) * maxX;
  const randomY = Math.random() * maxY;

  noTipRef.value.$el.style.position = "fixed";
  noTipRef.value.$el.style.left = `${randomX}px`;
  noTipRef.value.$el.style.top = `${randomY}px`;

  fifteen.value += 1;
  twenty.value += 1;
  twentyFive.value += 1;
  fourty.value += 1;
}

function handleTipClick(event: MouseEvent) {
  var topButtonRect = noTipRef.value.getBoundingClientRect();
  var isClickOnTopButton =
    event.clientX >= topButtonRect.left &&
    event.clientX <= topButtonRect.right &&
    event.clientY >= topButtonRect.top &&
    event.clientY <= topButtonRect.bottom;

  if (isClickOnTopButton) {
    return;
  }
  loading.value = true;
  noTipRef.value.$el.style.position = "";
  noTipRef.value.$el.style.left = "";
  noTipRef.value.$el.style.top = "";
  noTipRef.value.$el.style.width = "";
  setTimeout(() => {
    loading.value = false;
    fifteen.value = 15;
    twenty.value = 20;
    twentyFive.value = 25;
    fourty.value = 40;
  }, 3000);
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
    "fourty fourty fourty"
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
.fourty {
  grid-area: fourty;
}
.no-tip {
  grid-area: no-tip;
  z-index: 999;
}
.custom {
  grid-area: custom;
}
h1 {
  font-family: "Arial", sans-serif;
  font-weight: 200;
}
</style>
