<template>
  <v-container
    class="parent d-flex align-center justify-center"
    style="height: 100vh"
  >
    <v-card style="width: 500px" variant="tonal">
      <!-- Head -->

      <v-col cols="12" class="d-flex align-center justify-space-between px-0">
        <strong
          style="
            font-size: 26px;
            font-weight: 700;
            color: var(--color-txt);
            letter-spacing: 1px;
          "
          >calc</strong
        >
        <span
          style="
            font-size: 10px;
            font-weight: 700;
            color: var(--color-txt);
            letter-spacing: 1px;
          "
          >THEME
          <div class="switch">
            <div class="switch-radios">
              <input
                type="radio"
                name="theme-type"
                value="one"
                id="first"
                v-model="selectedTheme"
              />
              <input
                type="radio"
                name="theme-type"
                value="two"
                id="second"
                v-model="selectedTheme"
              />
              <input
                type="radio"
                name="theme-type"
                value="three"
                id="third"
                v-model="selectedTheme"
              />
            </div>
            <div class="ball" :style="{ left: ballPosition }"></div>
          </div>
        </span>
      </v-col>

      <!-- Screen -->

      <v-col cols="12" class="px-0 pb-6">
        <v-card
          color="var(--bg-screen)"
          class="py-5 px-5 text-right"
          style="font-size: 36px; color: var(--color-txt)"
          >{{ num1 }}</v-card
        >
      </v-col>

      <!-- KeyPad -->

      <v-card color="var(--bg-toggle)" class="px-4 py-6">
        <v-row>
          <v-col v-for="(key, index) in keys" :key="index" cols="3">
            <v-btn
              @click="addNum(key)"
              height="60"
              width="100%"
              :ripple="key === 'DEL' ? true : false"
              :color="`${
                key === 'DEL' ? 'var(--del-res-key)' : 'var(--bg-keys)'
              }`"
              :style="`font-size: 26px; color:${
                key === 'DEL' ? 'var(--color-screen)' : 'var(--color-nm)'
              }`"
              >{{ key }}</v-btn
            >
          </v-col>

          <!-- Buttom -->

          <v-col cols="6" v-for="(key, index) in act" :key="index">
            <v-btn
              @click="action(key)"
              height="50"
              width="100%"
              style="color: var(--color-screen); font-size: 26px"
              :color="`${
                key === 'RESET' ? 'var(--del-res-key)' : 'var(--egal-key)'
              }`"
              >{{ key }}</v-btn
            >
          </v-col>
        </v-row>
      </v-card>
    </v-card>
  </v-container>
</template>

<script setup>
import { ref, watchEffect } from "vue";

// ---- Theme Logic ---- //

const selectedTheme = ref("one");
const ballPosition = ref("4px");

watchEffect(() => {
  switch (selectedTheme.value) {
    case "one":
      ballPosition.value = "4px";
      document.documentElement.setAttribute("data-theme", "one");
      // document.body.classList.remove("sun", "meteor");
      break;
    case "two":
      ballPosition.value = "38px";
      document.documentElement.setAttribute("data-theme", "two");
      // document.body.classList.remove("moon", "meteor");
      // document.body.classList.add("sun");
      break;
    case "three":
      ballPosition.value = "72px";
      document.documentElement.setAttribute("data-theme", "three");
      // document.body.classList.remove("moon", "sun");
      // document.body.classList.add("meteor");
      break;
  }
});

// ---- Calc Logic ---- //

const num1 = ref(0);
const num2 = ref(null);
const numArr1 = ref([]);
const keysFilter = ref("");

const addNum = (key) => {
  if (key != "+" && key != "-" && key != "x" && key != "/") {
    numArr1.value.push(key);

    num1.value = numArr1.value.join("");
  } else {
    localStorage.setItem("1st", num1.value);

    numArr1.value = [];

    keysFilter.value = key;
  }
};

const action = (key) => {
  if (localStorage.getItem("1st")) {
    num2.value = JSON.parse(localStorage.getItem("1st"));

    if (key === "=") {
      if (keysFilter.value === "+") {
        num1.value = num2.value + parseFloat(num1.value);
      } else if (keysFilter.value === "-") {
        num1.value = parseFloat(
          (num2.value - parseFloat(num1.value)).toFixed(1)
        );
        console.log(num1.value);
      } else if (keysFilter.value === "x") {
        num1.value = num2.value * parseFloat(num1.value);
      } else {
        num1.value = num2.value / parseFloat(num1.value);
      }
    } else {
      localStorage.clear();
      numArr1.value = [];
      num1.value = 0;
    }
  }
};

const keys = ref([
  7,
  8,
  9,
  "DEL",
  4,
  5,
  6,
  "+",
  1,
  2,
  3,
  "-",
  ".",
  0,
  "/",
  "x",
]);

const act = ref(["RESET", "="]);
</script>

<style scoped>
.switch {
  height: 30px;
  width: 100px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: column;
  background-color: var(--bg-toggle);
  border-radius: 50px;
  padding: 5px;
  position: relative;
  cursor: pointer;
}

.switch-radios {
  position: relative;
}

.switch-radios > * {
  position: absolute;
}

input[type="radio"]:first-of-type {
  right: 22px;
}

input[type="radio"]:nth-of-type(2) {
  right: -10px;
}

input[type="radio"]:last-of-type {
  right: -42px;
}

.ball {
  background: var(--egal-key);
  height: 24px;
  width: 24px;
  border-radius: 50%;
  position: absolute;
  left: 4px;
  top: 3px;
  transition: all 0.5s ease;
}

input[type="radio"] {
  cursor: pointer;
  opacity: 0;
}

.parent >>> .v-card__underlay {
  display: none;
}
</style>
