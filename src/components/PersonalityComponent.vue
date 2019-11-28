<template>
  <div class="main text-center">
    <h1>{{ msg }}</h1>
    <p>{{ msg2 }}</p>
    <div class="mb-4">
      <input type="text" v-model="username" @keyup.enter="findUser" />
    </div>
    <div id="table_id">
      <table class="table striped" v-if="seen">
        <tbody>
          <tr>
            <td>Album</td>
            <td>Enlace</td>
          </tr>
          <tr v-for="a in albums" :key="a.id">
            <td>{{ a.album }}</td>
            <td><b-link :href="a.link">{{ a.link }}</b-link></td>
          </tr>
        </tbody>
      </table>
    </div>
    <div>
      <p>{{ albums }}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: "PersonalityComponent",
  props: {
    msg: String,
    msg2: String
  },
  data() {
    return {
      albums: null,
      errors: [],
      username: "",
      seen: false
    };
  },
  methods: {
    async findUser() {
      if (this.username == "") {
        alert("Por favor ingrese el nombre del usuario");
      } else {
        alert("https://personality-tweets-api.herokuapp.com/api/v1/" + this.username);
        await axios
          .get(
            "https://personality-tweets-api.herokuapp.com/api/v1/" +this.username)
          .then(response => {
            this.albums = response.data;
            //console.log(this.albums);
            if (this.albums == null) {
              alert("El usuario no puede ser analizado");
            }else{
              this.seen = true 
            }
          })
          .catch(e => alert(e));
      }
    }
  }
};

/*
{ "0": { "album": "Fearless", "link": "https://www.last.fm/music/Taylor+Swift" }, "1": { "album": "Born This Way", "link": "https://www.last.fm/music/Lady+Gaga" }, "2": { "album": "JOANNE (Deluxe)", "link": "https://www.last.fm/music/Lady+Gaga" }, "3": { "album": "Dangerous Woman", "link": "https://www.last.fm/music/Ariana+Grande" }, "4": { "album": "Speak Now", "link": "https://www.last.fm/music/Taylor+Swift" }, "5": { "album": "Teenage Dream", "link": "https://www.last.fm/music/Katy+Perry" }, "6": { "album": "American IV: The Man Comes Around", "link": "https://www.last.fm/music/Johnny+Cash" }, "7": { "album": "One of the Boys", "link": "https://www.last.fm/music/Katy+Perry" }, "8": { "album": "Taylor Swift", "link": "https://www.last.fm/music/Taylor+Swift" }, "9": { "album": "Bionic", "link": "https://www.last.fm/music/Christina+Aguilera" }, "10": { "album": "Red (Deluxe Version)", "link": "https://www.last.fm/music/Taylor+Swift" }, "11": { "album": "1989 (Deluxe)", "link": "https://www.last.fm/music/Taylor+Swift" } }
*/
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
