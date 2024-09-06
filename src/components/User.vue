<script>
export default {
  name: 'UserComponent',
  props: {
    user: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      msgColor: '#888888',
      message: '',
      userId: ''
    }
  },
  methods: {
    sendMessage(e) {
      console.log('enviaste un mensaje')
      console.log(this.msgColor)
      console.log(this.message)
      e.preventDefault
      if (this.user.msgColor && this.user.message) {
        this.$emit('add-message', { ...this.user })
      }
    }
  }
}
</script>

<template>
  <div v-if="user">
    <img :src="user.picture" :alt="user.firstName + user.lastName" />
    <h3>{{ user.firstName }} {{ user.lastName }}</h3>
    <input type="color" v-model="msgColor" />
    <textarea
      name="message"
      id="message"
      cols="10"
      rows="7"
      v-model="message"
      placeholder="Envia tu mensaje"
    ></textarea>
    <button @click="sendMessage()">Enviar</button>
  </div>
  <div v-else>
    <p>Cargando usuario</p>
  </div>
</template>

<style scoped>
input,
textarea,
button,
img {
  width: 100%;
}
</style>
