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
      id: ''
    }
  },
  methods: {
    sendMessage() {
      if (this.msgColor && this.message) {
        this.id = Date.now()
        this.$emit('add-message', {
          userId: this.user.userId,
          message: this.message,
          msgColor: this.msgColor
        })
        this.message = ''
      }
    },
    updateColor() {
      this.$emit('update-color', {
        userId: this.user.userId,
        color: this.msgColor
      })
    }
  }
}
</script>

<template>
  <div v-if="user">
    <img :src="user.picture" :alt="user.firstName + ' ' + user.lastName" />
    <h3>{{ user.firstName }} {{ user.lastName }}</h3>
    <input type="color" v-model="msgColor" @input="updateColor" />
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
