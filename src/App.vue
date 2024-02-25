<template>
  <calCulator />
</template>

<script setup>
import calCulator from "./components/Calculator.vue";
</script>

<style>
:root {
  font-family: "League Spartan", sans-serif;
  font-weight: 700;

  color: #ffffff;
  background-color: var(--main-bg);

  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;

  --main-bg: #3a4764;
  --bg-toggle: #232c43;
  --bg-screen: #182034;

  --del-res-key: #637097;
  --egal-key: #d03f2f;
  --bg-keys: #eae3dc;

  --color-txt: #ffffff;
  --color-screen: #ffffff;
  --color-nm: #444b5a;
}

[data-theme="two"] {
  --main-bg: hsl(0, 0%, 90%);
  --bg-toggle: hsl(0, 5%, 81%);
  --bg-screen: hsl(0, 0%, 93%);

  --del-res-key: hsl(185, 42%, 37%);
  --egal-key: hsl(25, 98%, 40%);
  --bg-keys: hsl(45, 7%, 89%);

  --color-txt: #35352c;
  --color-screen: #ffffff;
  --color-nm: #35352c;
}

[data-theme="three"] {
  --main-bg: hsl(268, 75%, 9%);
  --bg-toggle: hsl(268, 71%, 12%);
  --bg-screen: hsl(268, 71%, 12%);

  --del-res-key: hsl(281, 89%, 26%);
  --egal-key: hsl(176, 100%, 44%);
  --bg-keys: hsl(268, 47%, 21%);

  --color-txt: hsl(52, 100%, 62%);
  --color-screen: #ffffff;
  --color-nm: hsl(52, 100%, 62%);
}
</style>
