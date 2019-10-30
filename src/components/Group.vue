<template>
  <div id="Group">
    <button @click="play">PLAY</button><br>
    <button @click="form(0)">
      <span class="group-names">{{group.participant_0.first_name}}</span>
    </button><br>
    <button @click="form(1)">
      <span class="group-names">{{group.participant_1.first_name}}</span>
    </button><br>
    <button @click="form(2)">
      <span class="group-names">{{group.participant_2.first_name}}</span>
    </button><br>
    <button @click="form(3)">
      <span class="group-names">{{group.participant_3.first_name}}</span>
    </button><br>
    <button @click="back">Back</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Group",
  props: ["group", "password"],
  data: function() {
    return {};
  },
  methods: {
    form(participant_index) {
      this.$emit("form", participant_index, this.group.group_id);
    },
    back() {
      this.$emit("back");
    },
    play() {
      const options = {
        method: "PUT",
        headers: {
          "content-type": "application/x-www-form-urlencoded",
          accesskey: this.password
        },
        url: "https://shoreportal.com/tab_spring/api/groups/stop_all/"
      };
      axios(options);
      const params = new URLSearchParams();
      params.append("group_id", this.group.group_id);
      const options2 = {
        method: "POST",
        headers: {
          "content-type": "application/x-www-form-urlencoded",
          accesskey: this.password
        },
        data: params,
        url: "https://shoreportal.com/tab_spring/api/groups/play/"
      };
      axios(options2).then(() => {
        this.$emit("play");
      });
    }
  },
  mounted() {}
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
  font-size: 4vmin;
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