<script>
import { ref } from 'vue'
import axios from 'axios'
import Contacts_Container from './components/Contacts-container.vue'
import Chat from './components/Chat.vue'

export default {
  name: 'App',
  components: {
    Contacts_Container,
    Chat
  },

  created() {
    axios.get(`https://ott-fogliata.github.io/vuejs-s2i-repository/chat.json`).then(res => {
      this.$store.state.contacts = res.data
      this.$store.state.nameToDisplay = res.data[0].name
      this.$store.state.messagesToDisplay = res.data[0].messages
    }).catch(err => {
      console.log(err)
    })
  }
}

</script>

<template>
  <div class="flex flex-row h-screen">
    <Contacts_Container class="basis-1/4 bg-zinc-900"></Contacts_Container>
    <Chat class="basis-3/4 bg-zinc-800"></Chat>
  </div>
</template>
