// pages/index.vue
<template>
  <div class="h-screen flex items-center justify-center bg-gray-900 text-white">
    <div class="grid grid-cols-3 gap-4 w-full max-w-4xl">
      <!-- Neo Brutalist Calculator -->
      <NuxtLink to="/todo" class="flex flex-col items-center justify-center h-80 bg-white text-black border-4 border-black shadow-[8px_8px_0px_0px_rgba(0,0,0,1)] transition-transform hover:translate-x-1 hover:translate-y-1">
        <h2 class="text-2xl font-bold">To Do List</h2>
        <p class="text-sm">Neo Brutalist Style</p>
      </NuxtLink>
      
      <!-- Tokyo Night Theme -->
      <NuxtLink to="/calculator" class="flex flex-col items-center justify-center h-80 bg-[#1a1b26] text-[#82aaff] border border-[#3b4252] shadow-lg">
        <h2 class="text-2xl font-bold">Calculator</h2>
        <p class="text-sm">Tokyo Night Theme</p>
      </NuxtLink>
      
      <!-- Breaking Bad Tic Tac Toe -->
      <NuxtLink to="/ttt" class="flex flex-col items-center justify-center h-80 bg-[#1c1c1c] text-[#b5a642] border border-[#b5a642] shadow-md">
        <h2 class="text-2xl font-bold">Tic Tac Toe</h2>
        <p class="text-sm">Breaking Bad Theme</p>
      </NuxtLink>
    </div>
  </div>
</template>