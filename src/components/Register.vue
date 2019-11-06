<template>
  <div id="register">
    <button @click="create"><span id="plus">+</span></button>
    <br><br>
    <div v-for="group in groups" :key="group._id" >
      <button @click="selectGroup(group)">
        <img v-if=group.playing id="playing-icon" src="../assets/images/Playing.png" /><span class="group-names">{{group.participant_0.first_name + ", " + group.participant_1.first_name + ", " + group.participant_2.first_name + ", " + group.participant_3.first_name}}</span>
      </button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Register",
  props: ["password"],
  data: function() {
    return {
      groups: [],
      participants: []
    };
  },
  methods: {
    create() {
      const options = {
        method: "POST",
        headers: {
          "content-type": "application/x-www-form-urlencoded",
          accesskey: this.password
        },
        url: "https://shoreportal.com/tab_spring/api/groups/create/"
      };
      axios(options).then(response => {
        const new_group = {
          playing: response.data.group.playing,
          group_id: response.data.group._id,
          participant_0: {first_name: "_"},
          participant_1: {first_name: "_"},
          participant_2: {first_name: "_"},
          participant_3: {first_name: "_"}
        };
        this.selectGroup(new_group);
      });
    },
    selectGroup(group) {
      
      this.$emit("select-group", group);
    }
  },
  mounted() {
    const params = new URLSearchParams();
    params.append("participant_id", "null");
    const options = {
      method: "GET",
      headers: {
        "content-type": "application/x-www-form-urlencoded",
        accesskey: this.password
      },
      url: "https://shoreportal.com/tab_spring/api/groups/get/"
    };
    axios(options).then(response => {
      for (let group of response.data.groups) {
        let new_group = {
          playing: group.playing,
          group_id: group._id,
          participant_0: null,
          participant_1: null,
          participant_2: null,
          participant_3: null
        };
        const params = new URLSearchParams();
        params.append("participant_id", group.participant_0);
        const options = {
          method: "POST",
          headers: {
            "content-type": "application/x-www-form-urlencoded",
            accesskey: this.password
          },
          data: params,
          url: "https://shoreportal.com/tab_spring/api/participants/get/"
        };
        axios(options).then(response => {
          new_group.participant_0 = response.data;
          const params = new URLSearchParams();
          params.append("participant_id", group.participant_1);
          const options = {
            method: "POST",
            headers: {
              "content-type": "application/x-www-form-urlencoded",
              accesskey: this.password
            },
            data: params,
            url: "https://shoreportal.com/tab_spring/api/participants/get/"
          };
          axios(options).then(response => {
            new_group.participant_1 = response.data;
            const params = new URLSearchParams();
            params.append("participant_id", group.participant_2);
            const options = {
              method: "POST",
              headers: {
                "content-type": "application/x-www-form-urlencoded",
                accesskey: this.password
              },
              data: params,
              url: "https://shoreportal.com/tab_spring/api/participants/get/"
            };
            axios(options).then(response => {
              new_group.participant_2 = response.data;
              const params = new URLSearchParams();
              params.append("participant_id", group.participant_3);
              const options = {
                method: "POST",
                headers: {
                  "content-type": "application/x-www-form-urlencoded",
                  accesskey: this.password
                },
                data: params,
                url: "https://shoreportal.com/tab_spring/api/participants/get/"
              };
              axios(options).then(response => {
                new_group.participant_3 = response.data;
                this.groups.push(new_group);
              });
            });
          });
        });
      }
    });

    /*

    axios
      .get("https://shoreportal.com/tab_spring/api/groups/get", config)
      .then(response => {
        for (let group of response.data.groups) {
          //console.log(group)
          let new_group = {
            group_id: group.group_id,
            participant_0: "",
            participant_1: "",
            participant_2: "",
            participant_3: ""
          };
   
          axios
            .post(
              "https://shoreportal.com/tab_spring/api/participants/get",
              { participant_id: "5db287066807300bbb782881" },
              config
            )
            .then(response => {
              new_group.participant_0 = response.data.first_name;
              axios
                .post(
                  "https://shoreportal.com/tab_spring/api/participants/get",
                  { participant_id: "5db287066807300bbb782881" },
                  config
                )
                .then(response => {
                  new_group.participant_1 = response.data.first_name;
                  axios
                    .post(
                      "https://shoreportal.com/tab_spring/api/participants/get",
                      { participant_id: "5db287066807300bbb782881" },
                      config
                    )
                    .then(response => {
                      new_group.participant_2 = response.data.first_name;
                      axios
                        .post(
                          "https://shoreportal.com/tab_spring/api/participants/get",
                          { participant_id: "5db287066807300bbb782881" },
                          config
                        )
                        .then(response => {
                          new_group.participant_3 = response.data.first_name;
                          this.groups.push(new_group);
                        });
                    });
                });
            });
        }
      });

      */
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#register {
  margin-top: 20vmin;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
#playing-icon {
  height: 2vmin;
  display: inline-block;
  width: auto;
  margin-left: 0.1vmin;
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
}

.group-names {
  font-size: 4vmin;
  height: 5.5vmin;
  text-align: center;
  float: right;
  line-height: 5.5vmin;
  color: darkgreen;
  font-family: gilroy_regular;
}

#plus {
  font-family:'Courier New', Courier, monospace;
  font-size: 9vmin;
  line-height: 6.5vmin;
  font-weight: bold;
  color: darkgreen;
}
</style>
