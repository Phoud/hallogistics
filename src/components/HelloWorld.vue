<template>
  <div>
    <div class="columns">
      <div class="column is-8 is-offset-2">
        <div class="field">
          <label class="label is-pulled-left">ເລກໃບບິນ</label>
          <div class="control">
            <input class="input" v-model="parcelId" type="text" placeholder="ເລກໃບບິນ">
          </div>
        </div>
        <button class="button is-primary is-big" v-on:click="toClick()">ກວດສອບພັດສະດຸ</button>
        <hr>
        <table class="table is-fullwidth" v-if="status != false">
          <thead>
            <tr>
              <th>ວັນທີ ແລະເວລາ</th>
              <th>ສະຖານະ</th>
              <th>ສາງ</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="track in data">
              <th>{{ track.date }}</th>
              <th>{{ track.details }}</th>
              <th>{{ track.place }}</th>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

  </div>
</template>

<script>
  import axios from 'axios';
  export default {
    name: 'HelloWorld',
    data () {
      return {
        data:'',
        parcelId:'',
        status: false
      }
    },
    methods:{
      getData(){
        axios.get("https://cors-anywhere.herokuapp.com/http://trackhal.com/cgi-bin/GInfo.dll?EmsApiTrack&ntype=10000&cno="+this.parcelId).then(
          res => {      
      
      this.data = res.data.trackingEventList;
      // console.log(res.data.trackingEventList);



    });
      },
      toClick(){
        this.getData();
        this.status = true
      }
    },
    created(){
      
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url(http://fonts.googleapis.com/earlyaccess/notosanslao.css);
*{
  font-family: 'Noto Sans Lao', Saysettha OT, Phetsarath OT, sans-serif;
}
h1, h2 {
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
  color: #42b983;
}
</style>
