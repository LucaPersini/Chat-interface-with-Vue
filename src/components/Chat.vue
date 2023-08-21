<script>
import Message from './Message.vue'
import { ref } from 'vue'
import { useStore } from 'vuex'

export default {
  name: 'Chat',
  components: {
    Message
  },
  props: {
    messages: Array
  },
  setup() {
    const store = useStore()
    let input = ref('')

    function sendMessage() {
      let message = {
        date: getDate(),
        message: input.value,
        status: 'sent'
      }

      store.state.messagesToDisplay.push(message)
      input.value = ''

      scrollToBottom()
      getResponse()
    }

    function getDate() {
      const date = new Date()
      const year = date.getFullYear()
      const month = date.getMonth()
      const day = date.getDate()
      const hours = date.getHours()
      const minutes = date.getMinutes()
      const seconds = date.getSeconds()

      let newDate = `${year}-${month}-${day} ${hours}:${minutes}:${seconds}`

      return newDate
    }

    function getResponse() {
      let response = {
        date: getDate(),
        message: "Ciao! Grazie per avermi scritto",
        status: "received"
      }

      store.state.contacts.forEach(contact => {
        if (contact.name == store.state.nameToDisplay) {
          setTimeout(function () {
            contact.messages.push(response)
            scrollToBottom()
          }, 5000)
        }
      });
    }

    function scrollToBottom() {
      const chat = document.querySelector('#chat')
      setTimeout(function () {
        chat.scrollTo(0, chat.scrollHeight)
      }, 2)

    }

    return {
      sendMessage,
      input,
      scrollToBottom
    }
  }
}
</script>

<template>
  <div class="container flex flex-col relative">
    <div class="container p-10 flex flex-row items-center h-fit sticky">
      <div class="container px-3 bg-slate-300 w-10 h-10 flex items-center rounded-full justify-center">
        <i class="fa-regular fa-user text-zinc-900 text-lg"></i>
      </div>
      <h2 class="text-white text-3xl px-6">{{ this.$store.state.nameToDisplay }}</h2>
    </div>
    <div class="container overflow-auto h-auto mb-20" id="chat">
      <div class="container p-6" v-for="messages in this.$store.state.messagesToDisplay">
        <Message :messages="messages" />
      </div>
    </div>
    <div class="container bg-zinc-950 mt-6 p-5 h-fit absolute bottom-0 ">
      <form>
        <input v-model='input' class="rounded-s-full py-2 px-4 bg-zinc-800 text-white focus:outline-none w-11/12"
          type="text" placeholder="Type a message">
        <button @click.prevent="sendMessage"
          class="text-white bg-zinc-800 border border-l-2 border-zinc-950 w-1/12 rounded-e-full py-2 active:bg-zinc-700">
          <i class="fa-solid fa-paper-plane"></i>
        </button>
      </form>
    </div>
  </div>
</template>