<template>
    <!-- <ons-gesture-detector> -->
  <div id="signon" v-on:swipeleft="gochoose" v-on:swiperight="goscoreboard" v-on:swipebottom="gogamemaster">
    
    <!-- submit button -->
    <div class="form-group">
      <label for="usr">
      <!-- <svg data-v-8e11165c="" viewBox="0 0 425 300"><path data-v-8e11165c="" id="curve" d="M6,150C49.63,93,105.79,36.65,156.2,47.55,207.89,58.74,213,131.91,264,150c40.67,14.43"></path>
       <text style="stroke: red;
    text-shadow: -.5vw -1px 0 #000, 1px -1px 0 #000, -1px 1px 0 #000, 1px 1px 0 #000;"
             data-v-8e11165c="" x="80"><textPath data-v-8e11165c="" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#curve">
              Enter Your Gamer tag
            </textPath></text></svg> -->
        <span class="red">E</span><span class="green">n</span><span class="yellow">t</span><span class="blue">e</span><span class="red">r</span>
        <span class="green">Y</span><span class="yellow">o</span><span class="blue">u</span><span class="red">r</span>
        <span class="blue">N</span><span class="green">a</span><span class="yellow">m</span><span class="blue">e</span>

          <!-- <span class="yellow">Enter</span> <span class="green">your</span> <span class="red"> name</span> -->
       </label>
      <input type="text" class="form-control" id="usr" v-model="username">
    </div>
     <button type="button" class="go-btn btn" @click="signon()">Go!</button>

    <div @click="signon()">
    <img  class="mario" src="../assets/mario-running.gif"/>
    </div>
  </div>
      <!-- </ons-gesture-detector> -->
</template>

<script>
import CommonUtils from "./common-utils";
export default {
  name: "signin",
  mixins: [CommonUtils],
  // lifecycle callbacks
  beforeCreate() {
    document.body.className = 'mario';
  },
  created() {
    // instance created and data bound
    // looking for existing player information from local storage and prepopulate username
    let userInfo = this.retrieveFromStorage(
      "localStorage",
      "trouble_flipper_player"
    );
    if (userInfo && userInfo.username) {
      this.username = userInfo.username;
    }
  },
  // mounted() {
  //   console.log('signin mounted: dom element inserted');
  // },
  // beforeUpdate() {
  //   // add any customized code before DOM is re-render and patched based changes in data
  //   console.log('signin beforeUpdate: data is changed, about to rerender dom');
  // },
  // updated() {
  //   console.log('signin updated: dom is rerendered');
  // },
  destroyed() {
    // clean up any resource, such as close websocket connection, remove subscription
  },

  // Underlying model
  data() {
    return {
      msg: "Welcome to join Trouble Flipper!",
      user_type_list: [
        { text: "Player", value: "player" },
        { text: "Spectator", value: "spectator" },
        { text: "Game Master", value: "master" }
      ],
      username: "",
      password: "",
      usertype: "player"
    };
  },

  // any actions
  methods: {
    gochoose: function(event) {
      this.$router.push("game");
    },
    goscoreboard: function(event) {
      this.$router.push({
        name: "scoreboard",
        query: {
          username: this.username,
          isMaster: this.usertype === "master"
        }
      });
    },
    gogamemaster: function(event) {
      console.log("go as master login");
    },
    signon: function(event) {
      console.log(this.username + ", " + this.password + ", " + this.usertype);
      if (this.usertype === "player") {
        this.$router.push({
          name: "game",
          query: {
            username: this.username
          }
        });
      } else {
        this.$router.push({
          name: "scoreboard",
          query: {
            username: this.username,
            isMaster: this.usertype === "master"
          }
        });
      }
    },
    signout: function(event) {}
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- Enable sas by using lang="scss" -->
<style scoped>
h1,
h2 {
  font-weight: normal;
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
  color: #1dacfc;
}
#signon {
  height: 100%;
  flex: 1;
  align-self: stretch;
  display: flex;
  flex-direction: column;
  align-items: center;
}
label {
  font-size: 40px;
}
.center {
  text-align: center;
  width: 100%;
}

.form-group {
  margin: 100px auto 0 auto;
  text-align: center;
}

input {
  font-size: 32px;
  font-family: Roboto;
  text-align: center;
}

.mario {
  width: 200px;
  padding: 40px 0;
}

.go-action .label {
  position: absolute;
  bottom: 0;
  font-size: 32px;
  color: #006fea;
  left: calc(50% - 16px);

}
.go-action:hover  {
  border-radius: 300px;
  border: 1px solid #758291;
    box-shadow: -3px -1px 3px #afa1df,  -9px 2px 0 #afa1df, 5px 1px 0 #afa1df,
    10px 3px 0px 1px #afa1df;
}
.go-action  {
  position: relative;
  
  border-radius: 300px;
  border: 1px solid #758291;
    box-shadow: 3px -1px 3px #565151, 9px 2px 0 #c3acac, 5px 1px 0 #9c9292,
    10px 3px 0px 1px #a99191;
}
.go-btn {
  font-size: 32px;
  margin-bottom: 80px;
  background: #006fea;
  border-radius: 40px;
  padding: 10px;
  margin: 40px 0;
  color: white;
  width: 100px;
  min-height: 70px;
}

.red {
  color: #d41345;
  text-shadow: -3px -1px 0 #000, 1px -1px 0 #000, -1px 1px 0 #000,
    1px 1px 0 #000;
}
.blue {
  color: rgb(5, 139, 255);
  text-shadow: -3px -1px 0 #000, 1px -1px 0 #000, -1px 1px 0 #000,
    1px 1px 0 #000;
}

.yellow {
  color: rgb(255, 252, 0);
  text-shadow: -3px -1px 0 #000, 1px -1px 0 #000, -1px 1px 0 #000,
    1px 1px 0 #000;
}
.green {
  color: rgb(37, 173, 33);
  text-shadow: -3px -1px 0 #000, 1px -1px 0 #000, -1px 1px 0 #000,
    1px 1px 0 #000;
}
</style>
