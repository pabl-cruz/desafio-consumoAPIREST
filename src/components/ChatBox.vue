<script>
export default {
  name: 'ChatBoxComponent',
  props: {
    user1: {
      type: Object,
      required: true
    },
    user2: {
      type: Object,
      required: true
    },
    messages: {
      type: Array,
      required: true
    }
  },
  methods: {
    updateMessageColors(userId, color) {
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
  <div class="chatbox">
    <div
      v-for="(message, id) in messages"
      :key="id"
      class="msgFrame"
      :class="{
        msgLeft: message.userId === user1.userId,
        msgRight: message.userId === user2.userId
      }"
    >
      <p v-if="message.userId === user1.userId">{{ user1.firstName }}</p>
      <p v-else-if="message.userId === user2.userId">{{ user2.firstName }}</p>
      <div
        class="msgbox"
        :style="{
          backgroundColor:
            message.userId === user1.userId || message.userId === user2.userId
              ? message.msgColor
              : ''
        }"
      >
        <p>{{ message.message }}</p>
      </div>
    </div>
  </div>
</template>
<style scoped>
.chatbox {
  background-color: #d6e7e7;
  padding: 2rem;
  width: 50vw;
  height: 50vh;
  display: flex;
  flex-direction: column;
  overflow-y: auto;
}
.msgbox {
  margin: 1rem;
  padding: 0.75rem;
  font-size: 13px;
  border-radius: 20px;
  box-shadow: 1px 1px 8px 2px #969e9c;
  width: max-content;
}
.msgLeft {
  justify-content: flex-start;
  text-align: left;
}
.msgRight {
  flex-wrap: wrap-reverse;
  text-align: right;
}
.msgFrame {
  display: flex;
  flex-direction: column;
}
</style>
