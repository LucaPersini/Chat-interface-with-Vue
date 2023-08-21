<script>
export default {
  name: 'Contact',
  props: {
    name: String
  }
}
</script>

<template>
  <div
    class="container px-5 py-4 hover:bg-zinc-700 hover:cursor-pointer flex flex-row items-center border-b-2 border-zinc-800"
    :name="name">
    <div class="container px-3 bg-slate-300 w-10 h-10 flex items-center rounded-full justify-center">
      <i class="fa-regular fa-user text-zinc-900 text-lg"></i>
    </div>
    <h2 class="text-white text-xl px-3">{{ name }}</h2>
  </div>
</template>