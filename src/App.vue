<template>
  <div id="app">
    <Register v-if="state==='register'" @select-group="selectGroup" :password=password />
    <Group v-if="state==='group'" :group=group @form="form" @back="state='register'" @play="play" :password=password />
    <Form v-if="state==='form'" :participant_index="participant_index" :group_id="group_id" @register="state='register'" @back="state='group'" :password=password />
    <Play v-if="state==='play'" @stop="state='register'" :password=password />
  </div>
</template>

<script>
import Register from './components/Register.vue';
import Group from './components/Group.vue';
import Form from './components/Form.vue';
import Play from './components/Play.vue';

export default {
  name: 'app',
  data: function() {
    return {
      state: "",
      group: null,
      participant_index: null,
      group_id: null,
      password: null
    }
  },
  components: {
    Register,
    Group,
    Form,
    Play
  },
  methods: {
    play() {
      this.state='play';
    },
    selectGroup(group) {
      this.group = group;
      this.state = 'group';
    },
    form(participant_index, group_id) {
      this.participant_index = participant_index;
      this.group_id = group_id;
      this.state = 'form';
    },
  },
  mounted() {
    let password = prompt("Please enter the password", "");
    this.password = password;
    this.state = "register";
  }
}
</script>

<style>
* {
  outline: none;
}
@font-face {
  font-family: "gilroy_bold";
  src: url("./assets/fonts/Gilroy-Bold.ttf");
}
@font-face {
  font-family: "gilroy_heavy";
  src: url("./assets/fonts/Gilroy-Heavy.ttf");
}
@font-face {
  font-family: "gilroy_light";
  src: url("./assets/fonts/Gilroy-Light.ttf");
}
@font-face {
  font-family: "gilroy_medium";
  src: url("./assets/fonts/Gilroy-Medium.ttf");
}
@font-face {
  font-family: "gilroy_regular";
  src: url("./assets/fonts/Gilroy-Regular.ttf");
}
body {
  margin: 0;
  background: #0a672e;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
