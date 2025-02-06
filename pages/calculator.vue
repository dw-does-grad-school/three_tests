// components/Calculator.vue
<template>
  <!-- Return Home Button -->
  <router-link
    to="/"
    class="fixed top-4 left-4 bg-[#ff5370] text-white font-bold py-2 px-4 rounded hover:bg-[#ff7a80] transition"
  >
    Return Home
  </router-link>

  <div class="flex justify-center items-center h-screen bg-[#1a1b26]">
    <div class="w-80 bg-[#222436] p-4 rounded-2xl shadow-lg border border-[#2e3440]">
      <!-- Display -->
      <div class="text-right text-white text-2xl p-3 bg-[#1a1b26] rounded-lg mb-4 shadow-inner">
        {{ currentInput || "0" }}
      </div>
      
      <!-- Buttons Grid -->
      <div class="grid grid-cols-4 gap-2">
        <button
          v-for="button in buttons"
          :key="button.label"
          class="py-3 text-xl font-bold rounded-lg shadow-md transition-all"
          :class="getButtonClass(button.label)"
          @click="handleClick(button.label)"
        >
          {{ button.label }}
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const currentInput = ref("");

const buttons = [
  { label: "C" }, { label: "⌫" }, { label: "%" }, { label: "/" },
  { label: "7" }, { label: "8" }, { label: "9" }, { label: "*" },
  { label: "4" }, { label: "5" }, { label: "6" }, { label: "-" },
  { label: "1" }, { label: "2" }, { label: "3" }, { label: "+" },
  { label: "0" }, { label: "00" }, { label: "." }, { label: "=" }
];

const handleClick = (label) => {
  if (label === "C") return (currentInput.value = "");
  if (label === "⌫") return (currentInput.value = currentInput.value.slice(0, -1));
  if (label === "=") return evaluateExpression();
  currentInput.value += label;
};

const evaluateExpression = () => {
  try {
    // Using eval here for simplicity; in production consider a safer alternative.
    currentInput.value = eval(currentInput.value).toString();
  } catch (error) {
    currentInput.value = "Error";
  }
};

const getButtonClass = (label) => {
  if (["C", "⌫"].includes(label)) return "bg-[#ff5370] text-white";
  if (["/", "*", "-", "+", "%"].includes(label)) return "bg-[#82aaff] text-white";
  if (label === "=") return "bg-[#c3e88d] text-black col-span-2";
  return "bg-[#2e3440] text-white hover:bg-[#3b4252]";
};
</script>
