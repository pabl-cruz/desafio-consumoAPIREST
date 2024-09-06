<script>
import axios from 'axios'
import UserComponent from '@/components/User.vue'
import ChatBoxComponent from '@/components/ChatBox.vue'
export default {
  components: {
    UserComponent,
    ChatBoxComponent
  },
  data() {
    return {
      usersData: '',
      messages: []
    }
  },
  async mounted() {
    try {
      const url = 'https://randomuser.me/api/?results=2'
      const { data } = await axios.get(url)
      this.usersData = data.results.map(({ name, picture }, index) => ({
        userId: index + 1,
        firstName: name.first,
        lastName: name.last,
        picture: picture.large
      }))
      console.log(this.usersData)
    } catch (error) {
      console.error(error)
    }
  },
  methods: {
    addMessage(msg) {
      this.messages.push(msg)
    }
  }
}
</script>

<template>
  <main>
    <h1>Chat</h1>
    <UserComponent :user="usersData[0]" @add-message="addMessage" />
    <ChatBoxComponent :user1="usersData[0]" :user2="usersData[1]" :messages="messages" />
    <UserComponent :user="usersData[1]" @add-message="addMessage" />
  </main>
</template>

<style scoped>
main {
  display: flex;
}
h1 {
  margin: 2rem;
  justify-content: center;
}
</style>
