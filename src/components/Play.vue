<template>
  <div id="play">
    <button @click="stop">BACK</button><br>
    <button @click="scene(1)">The Bird Cage</button><br>
    <button @click="scene(2)">The Mounting Yard</button><br>
    <button @click="scene(3)">Winning The Cup</button><br>
    <button @click="scene(4)">Meet Phar Lap</button><br>
    <button @click="snap">Snap</button>
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
button {
  -webkit-appearance: none;
  background: white;
  height: 5.5vmin;
  outline: none;
  border: 0.1vmin solid black;
  border-radius: 1vmin;
  padding: 0.3vmin;
  margin: 0.25vmin 0;
}

.group-names {
  font-size: 3vmin;
  height: 5.5vmin;
  text-align: center;
  display: inline-block;
  float: right;
  line-height: 5.5vmin;
}

#plus {
  font-size: 5vmin;
  display: inline-block;
  float: left;
  line-height: 5vmin;
}
</style>