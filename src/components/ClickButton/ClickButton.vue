<template>
  <v-main class="mt-2">
    <v-card @click.left="clickEvent" class="mx-auto clickCard" max-width="230">
      <v-chip size="large" class="ma-2">
        <v-icon icon="mdi-mouse-left-click" start></v-icon>
        Clicks: {{ clicks }}
      </v-chip>
      <v-chip size="large" class="ma-2" color="primary">
        <v-icon icon="mdi-mouse-left-click-outline" start></v-icon>
        Doubles: {{ doubles }}
      </v-chip>
      <v-chip size="large" class="ma-2" :color="fail ? 'orange' : 'primary'">
        <v-icon :icon="fail ? 'mdi-mouse-off' : 'mdi-shield-check'" start>
        </v-icon>
        Fail: {{ fail ? 'Yes' : 'No' }}
      </v-chip>
      <v-btn prepend-icon="mdi-restart" @click="reset" max-width="100">
        Reset
      </v-btn>
    </v-card>
  </v-main>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

let prevClickTime = 0;

function getClickTime() {
  const now = new Date().getTime() / 1000;
  const miliseconds = (now % 1)*1000;
  return miliseconds;
}

function reset() {
  clicks.value = -1;
  doubles.value = 0;
  fail.value = false;
}

function clickEvent(event: Event) {
  event.preventDefault()
  const clickTime = getClickTime();
  let diff = 0;
  (clickTime - prevClickTime) < 0 ?
    diff = 1000 - prevClickTime + clickTime :
    diff = clickTime - prevClickTime;
  if (diff < 80) {
    doubles.value++;
    fail.value = true;
  }
  clicks.value++
  prevClickTime = getClickTime();
}

let clicks = ref(0);
let doubles = ref(0);
let fail = ref(false);

</script>

<style scoped src="./ClickButton.scss"></style>