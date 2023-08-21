<script>
import Contact from './Contact.vue'
import { useStore } from 'vuex'
import { computed, ref } from 'vue'

export default {
  name: 'Contacts_Container',
  components: {
    Contact,
  },
  setup() {
    const store = useStore()
    let input = ref('')
    const nameToDisplay = computed(() => {
      return store.state.contacts.filter(contact => contact.name.toLowerCase().includes(input.value.toLowerCase()))
    })

    function setChat(name, messages) {
      store.state.nameToDisplay = name
      store.state.messagesToDisplay = messages
    }

    return {
      setChat,
      input,
      nameToDisplay
    }
  }
}
</script>

<template>
  <div class="container">
    <h1 class="text-white text-3xl font-semibold px-5 py-5">Chats</h1>
    <div class="container px-5 py-3">
      <form>
        <input @input="searchContact" v-model="input"
          class="py-1 px-3 rounded-full bg-zinc-800 focus:outline-none text-white w-full"
          style='font-family: Arial, FontAwesome;' type="text" placeholder="&#xf002; Search...">
      </form>
    </div>
    <div class="container">
      <div v-for="contact in nameToDisplay">
        <Contact :name='contact.name' @click="setChat(contact.name, contact.messages)" />
      </div>
    </div>
  </div>
</template>