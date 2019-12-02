<template>
  <div id="weather-container">
  	<div class="weather-textbox">
	  	<input type="text" placeholder="Search.." name="search2" ref ="textvalue" v-on:keyup.enter="getweather">
        <button type="submit" @click="getweather" ><i class="fa fa-search"></i></button>
	 </div>
	 <div class="weather-display-section"  ref ="displaysection">
	 	<img :src= imgsrc v-if="imgsrc">
	 	<div v-for="itm in items">	     	
	        <p v-if="itm.name"><span>Entered City is: </span>{{itm.name}}</p>
			<p v-if="itm.region"><span>Region: </span>{{itm.region}}</p>
			<p v-if="itm.humidity"><span>Humidity: </span>{{itm.humidity}}</p>
			<p v-if="itm.temperature"><span>Temperature: </span>{{itm.temperature}}</p>
	      </div>	
	 </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'weather',
 data () {
    return {
     items: null,
     errors: [],
     listOfObjects: null,
     imgsrc:null
    }
  },
  methods:{
  	getweather(){
  		console.log(this.$refs.textvalue.value);
  		const searchkeyword = this.$refs.textvalue.value;
        const apikey = 'e0b6267576917bb1dc04e0237c9d009e';
  		axios.get(`http://api.weatherstack.com/current?access_key=${apikey}&query=${searchkeyword}`)
	    .then(response => {
	     this.$refs.displaysection.style.display="block";
	     this.items = response.data;
	       console.log(response.data);
	       this.imgsrc = this.items.current.weather_icons[0];
		    })
	    .catch(e => {
	      this.errors.push(e)
	    })

  	}
  }
}
</script>
<style lang="scss" scoped>
  @import '../styles/weather.scss';
</style>
