<script>
export default {
  name: 'Message',
  props: {
    messages: Object
  }
}
</script>

<template>
  <div class="container" :messages="messages">
    <div class="container" v-if="messages.status == 'sent'">
      <div class="container flex justify-end">
        <div class="bg-zinc-600 w-fit p-3 rounded-md text-end">
          <h2 class="text-white">{{ messages.message }}</h2>
          <p class="text-gray-300">{{ messages.date }}</p>
        </div>
      </div>
    </div>
    <div class="container" v-else-if="messages.status == 'received'">
      <div class="container flex justify-start">
        <div class="bg-zinc-500 w-fit p-3 rounded-md text-start">
          <h2 class="text-white">{{ messages.message }}</h2>
          <p class="text-gray-300">{{ messages.date }}</p>
        </div>
      </div>
    </div>
  </div>
</template>