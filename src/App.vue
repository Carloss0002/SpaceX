<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center text-center">
          <h2>SpaceX Timeline</h2>
      </div>

      <v-spacer></v-spacer>
   
    <div v-if="launches.length < 0">
      Loading...
    </div>
    </v-app-bar>
    <div>
     <v-content>
       <v-container>
         <v-timeline v-if="launches.length > 0">
           <TimeLine v-for="launch in launches" :key="launch.flight_number" :launch="launch">

           </TimeLine>
         </v-timeline>
       </v-container>
     </v-content>
    </div>
    
  </v-app>
</template>

<script>
import axios from 'axios';
import TimeLine from './components/LaunchTime.vue'
export default {
  name: 'App',
  components:{
    TimeLine
  },
  data: () => ({
    launches:[]
  }),
  async created(){
    const {data} = await axios.get('https://api.spacexdata.com/v3/launches')
    data.forEach(launch =>{
      this.launches.push(launch)
    });
    console.log(this.launches)
  }
};
</script>
