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
  //al inicio de ciclio de vida se hace fetch a API randomuser.me
  async mounted() {
    try {
      const url = 'https://randomuser.me/api/?results=2'
      const { data } = await axios.get(url)
      //hacer un map de data para sacar solo nombre, apellido e imagen. se añade index a nuevo arreglo para identificador de usuario
      this.usersData = data.results.map(({ name, picture }, index) => ({
        userId: index + 1,
        firstName: name.first,
        lastName: name.last,
        picture: picture.large
      }))
    } catch (error) {
      console.error(error)
    }
  },
  methods: {
    //metodo de añadir mensajes, agregando a arreglo de messages
    addMessage(msg) {
      this.messages.push(msg)
    },
    //metodo para actualizar color de mensajes de un usuario para comunicar entre componente de usuario con el de chatbox
    updateColor({ userId, color }) {
      this.messages.forEach((msg) => {
        if (msg.userId === userId) {
          msg.msgColor = color
        }
      })
    }
  }
}
</script>

<template>
  <h1>Chat</h1>
  <br />
  <main>
    <!--llamado a componente de usuario, se asigna primer usuario de usersData, y emits a eventos personalizados para realizar comunicacion entre componentes-->
    <UserComponent :user="usersData[0]" @add-message="addMessage" @update-color="updateColor" />
    <!--llamado a componente de chatbox, se asignan usuarios y arreglo de mensajes-->
    <ChatBoxComponent :user1="usersData[0]" :user2="usersData[1]" :messages="messages" />
    <UserComponent :user="usersData[1]" @add-message="addMessage" @update-color="updateColor" />
  </main>
</template>

<style scoped>
main {
  display: flex;
}
h1 {
  margin: 2rem;
  text-align: center;
}
</style>
