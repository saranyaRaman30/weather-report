<template>
  <div id="weather-container">
  	<div class="weather-textbox">
	  	<input type="text" placeholder="Search.." name="search2" ref ="textvalue" v-on:keyup.enter="getweather">
        <button type="submit" @click="getweather" ><i class="fa fa-search"></i></button>
	 </div>
	 <div class="weather-display-section">
	 	<div class="show-weather-details">
     <div v-for="itm in items">
        <p>{{itm.name}}</p>
		<p>{{itm.region}}</p>
		<p>{{itm.humidity}}</p>
		<p>{{itm.temperature}}</p>
      </div>
	 		<!-- <p>{{listOfObjects}}</p> -->
	 		<!-- <p v-for="(value, key) in posts">{{ key }}</p> -->
	 		<ul>
		      <li v-for="(value, key) in listOfObjects">{{ key }}: {{ value }} </li>
		    </ul>
	 		
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
     listOfObjects: null
    }
  },
  methods:{
  	getweather(){
  		console.log(this.$refs.textvalue.value);
  		const searchkeyword = this.$refs.textvalue.value;
        const apikey = 'e0b6267576917bb1dc04e0237c9d009e';
  		axios.get(`http://api.weatherstack.com/current?access_key=${apikey}&query=${searchkeyword}`)
  		// .then(response => {
    //               this.items = () => JSON.parse(response.data);
    //               console.log('erere',this.items);
    //     })
	    .then(response => {
	      this.items = response.data;
	       console.log(response.data);
		    })
			// let listOfObjects = Object.keys(response.data).map((value,index) => {
			// 	return response.data[value]
			// 		console.log('erere',listOfObjects);
			// 	})
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
