<template>
  <div id="play">
    <button @click="stop">BACK</button><br>
    <hr>
    <button @click="scene(1)">The Bird Cage</button><br>
    <button @click="scene(2)">The Mounting Yard</button><br>
    <button @click="scene(3)">Winning The Cup</button><br>
    <button @click="scene(4)">Meet Phar Lap</button><br>
    <hr>
    <button @click="snap">SNAP</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Play",
  props: ["password"],
  methods: {
    stop() {
      this.$emit("stop");
    },
    scene(index) {
      const options = {
        method: "GET",
        headers: {
          "content-type": "application/x-www-form-urlencoded",
          accesskey: this.password
        },
        url: "https://shoreportal.com/tab_spring/api/plays/scene_" + index
      };
      axios(options);
    },
    snap() {
      const options = {
        method: "GET",
        headers: {
          "content-type": "application/x-www-form-urlencoded",
          accesskey: this.password
        },
        url: "https://shoreportal.com/tab_spring/api/plays/snap"
      };
      axios(options);
    }
  }
};
</script>

<style scoped>
#play {
  width: 40vmin;
  margin: auto;
  transform: translate(0, 50%);
}
button {
  -webkit-appearance: none;
  background: white;
  height: 8vmin;
  outline: none;
  border: 0.5vmin solid darkgreen;
  border-radius: 2vmin;
  margin: 0.25vmin 0;
  overflow: hidden;
  padding: 0.5vmin;
   font-size: 4vmin;
   line-height: 5.5vmin;
  color: darkgreen;
  font-family: gilroy_regular;
}


</style>