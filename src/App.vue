<template>
  <v-app>
    <v-container class="content-container d-flex flex-column align-center">
      <v-row class="w-100 justify-center">
        <v-col cols="12" class="d-flex justify-center align-center flex-wrap">
          <div v-for="(value, index) in counters" :key="index" class="counter-group mx-2">
            <v-btn @click="increment(index)" :class="['rect-button', 'pixel-border', getButtonColor(index)]"
              :aria-label="'Increase counter ' + (index + 1)"><v-icon>mdi-chevron-up</v-icon></v-btn>
            <div class="counter-wrapper">
              <v-card :class="['pa-0 pixel-font bordered-card pixel-border', getColorClass(index)]">
                <v-card-text class="text-center no-wrap number-text pa-0 my-4">{{ value }}</v-card-text>
              </v-card>
            </div>
            <v-btn @click="decrement(index)" :class="['rect-button', 'pixel-border', getButtonColor(index)]"
              :aria-label="'Decrease counter ' + (index + 1)"><v-icon>mdi-chevron-down</v-icon></v-btn>
          </div>
        </v-col>
      </v-row>
      <div class="pixel-text conduit-text text-center">I am a conduit for nonsense</div>

      <v-btn @click="confirmReset" color="red" class="reset-button pixel-border">Reset</v-btn>

      <v-dialog v-model="dialog" style="overflow: hidden;">
        <v-card class="pixel-border pa-4" style="overflow: hidden;">
          <v-card-title class="pixel-font text-center pa-0 mb-4">Are you sure you want to reset?</v-card-title>
          <v-card-actions class="d-flex justify-center pa-0">
            <v-btn v-for="(option, idx) in resetOptions" :key="idx" @click="option.action" :color="option.color"
              class="pixel-border mx-2">
              {{ option.label }}
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>

      <div class="pixel-text username text-center">@VelyxOCE</div>
    </v-container>
  </v-app>
</template>

<script setup>
import { ref, computed } from "vue";

const counters = ref([0, 0, 0]);
const dialog = ref(false);

const getColorClass = (index) => ["green-bar", "white-bar", "blue-bar"][index] || "default-button";
const getButtonColor = (index) => ["light-green-button", "light-grey-button", "light-blue-button"][index] || "default-button";

const increment = (index) => counters.value[index]++;
const decrement = (index) => {
  if (counters.value[index] > 0) counters.value[index]--;
};
const confirmReset = () => (dialog.value = true);
const resetCounters = () => {
  counters.value = [0, 0, 0];
  dialog.value = false;
};

const resetOptions = [
  { label: "Yes", action: resetCounters, color: "green" },
  { label: "No", action: () => (dialog.value = false), color: "red" },
];
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=VT323&display=swap");

html,
body,
#app,
.v-application {
  background-color: var(--bg-dark) !important;
  margin: 0;
  padding: 0;
  height: 100%;
}

.content-container {
  background-image: url("/Frog%203.png"), url("/Helga%20text.png");
  background-size: 50%, 30%;
  background-position: center left, top left;
  background-repeat: no-repeat, no-repeat;
  padding: 20px;
  min-height: 100vh;
  position: relative;
}

.pixel-font {
  font-family: "VT323", monospace;
  font-size: 36px;
  white-space: nowrap;
}

@media (max-width: 600px) {
  .pixel-font {
    font-size: 24px;
  }
}

@media (max-width: 400px) {
  .pixel-font {
    font-size: 20px;
  }
}

.pixel-text {
  font-family: "VT323", monospace;
  font-size: 24px;
  color: white;
  text-align: center;
  margin-top: 20px;
}

.conduit-text {
  position: relative;
  width: 100%;
  text-align: center;
  margin: 20px 0;
}

.username {
  margin-top: 10px;
  font-size: 20px;
}

.counter-group {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0 8px;
}

.counter-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
}

.bordered-card {
  background-color: var(--card-bg);
  width: 76px;
  text-align: center;
  font-family: "VT323", monospace;
  white-space: nowrap;
}

.green-bar {
  border: 2px solid var(--green-bar) !important;
  color: var(--green-bar) !important;
}

.white-bar {
  border: 2px solid var(--white-bar) !important;
  color: var(--white-bar) !important;
}

.blue-bar {
  border: 2px solid var(--blue-bar) !important;
  color: var(--blue-bar) !important;
}

.rect-button {
  height: 40px;
  width: 76px;
  min-width: 76px !important;
  max-width: 76px;
  text-transform: none;
  font-size: 24px;
  padding: 0;
  margin: 4px 0;
  align-self: flex-end;
  font-family: "VT323", monospace;
}

.no-wrap {
  white-space: nowrap;
}

.number-text {
  font-size: 48px !important;
}

.pixel-border {
  border: none;
  position: relative;
}

.pixel-border::before {
  content: "";
  position: absolute;
  top: -4px;
  left: -4px;
  right: -4px;
  bottom: -4px;
  background: none;
  box-shadow: -4px -4px 0 black, 4px -4px 0 black, -4px 4px 0 black,
    4px 4px 0 black;
  z-index: -1;
}

.reset-button {
  width: 200px;
  margin: 20px auto;
  font-size: 24px;
  font-family: "VT323", monospace;
  text-transform: none;
  background-color: red;
  color: white;
  display: block;
}
</style>
