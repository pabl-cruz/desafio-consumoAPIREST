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
  }
}
</script>
<template>
  <div class="chatbox">
    <div v-for="(message, id) in messages" :key="id">
      <p v-if="message.userId === user1.userId">{{ user1.firstName }}</p>
      <p v-else-if="message.userId === user2.userId">{{ user2.firstName }}</p>
      <div
        class="msgbox"
        :class="{
          bgUser1: message.userId === user1.userId,
          bgUser2: message.userId === user2.userId,
          msgLeft: message.userId === user1.userId,
          msgRight: message.userId === user2.userId
        }"
      >
        <p>{{ message.message }}</p>
      </div>
    </div>
  </div>
</template>
<style scoped>
.chatbox {
  background-color: #b1cccb;
  padding: 2rem;
  width: 50vw;
  height: 50vh;
  display: flex;
  flex-direction: column;
  overflow-y: scroll;
}
.msgbox {
  margin: 1rem;
  padding: 0.75rem;
  font-size: 13px;
}
.bgUser1 {
  background-color: cadetblue;
}
.bgUser2 {
  background-color: orange;
}
.msgLeft {
  justify-content: flex-start;
  text-align: left;
}
.msgRight {
  justify-content: flex-end;
  text-align: right;
}
</style>
