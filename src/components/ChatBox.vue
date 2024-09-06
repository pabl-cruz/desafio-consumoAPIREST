<script>
export default {
  name: 'ChatBoxComponent',
  props: {
    user1: {
      type: Object,
      required: true,
      userId: 1
    }
  },
  user2: {
    type: Object,
    required: true,
    userId: 2
  },
  data() {
    return {
      messages: []
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
  <div class="chatbox" v-for="(message, id) in messages" :key="id">
    <div
      class="msgbox"
      :class="{
        bg-user1: user == 0,
        bg-user2: user == 1,
        msg-left: user == 0,
        msg-right: user == 1,
    }"
    >
      <p>{{ message }}</p>
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
}
.textbox {
  margin: 1rem;
  padding: 0.75rem;
  font-size: 13px;
}
.bg-user1 {
  background-color: cadetblue;
}
.bg-user2 {
  background-color: orange;
}
.msg-left {
  justify-content: flex-start;
  text-align: left;
}
.msg-right {
  justify-content: flex-end;
  text-align: right;
}
</style>
