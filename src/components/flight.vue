<template>
    <div class="container bg-transparent m-auto mt-5 " >
        <!-- ROW1 -->
            <div class="row text-center bg-light mb-2">
                <h3 class="text-warning">FIND FLIGHT WITH US</h3>
            </div>
        <!-- ROW2 -->
            <div class="row text-center bg-light">
                <h4 class="text-info">Ready For your Next trip?Book With Us Now</h4>
            </div>
        <!-- ROW3 FOR SEARCH  -->
        <div class="row text-center bg-light mt-3">
                <!-- FORM  -->
            <div class="col d-box text-center" style="position: relative">
                    <br />
                    <span class="text-muted">
                        Leaving From <br />
                        <i class="fas fa-plane-departure"></i>
                    </span>
                    <br />
                    <br />
                    <div class="input-group mb-3">
                        <input v-model="from" type="text" class="form-control text-center" placeholder="FROM" aria-label="Departure"
                            @input="searchfrom()" />
                    </div>
                    <p id="fromcity"></p>
                    <div class="from-list" v-if="statusfrom" style="position: absolute; z-index: 1000"
                        id="flightfrom-list">
                        <table>
                            <tr  v-for="(list, index) in flight_from_api"
                                 :key="index"
                                 style="cursor: pointer; background-color: whitesmoke">
                                <td scope="col" @click="setFlightFrom(list)">
                                     <b> {{ list[1] }}</b> ,<b>{{ list[2] }}</b> ,
                                         {{ list[0] }}
                                </td>
                            </tr>
                        </table>
                    </div>
                </div>
                <!-- TO -->
            <div class="col d-box text-center" style="position: relative">
                    <br />
                    <span class="text-muted">
                        Going To <br />
                        <i class="fas fa-plane-arrival"></i>
                    </span>
                    <br />
                    <br />
                    <div class="input-group mb-3">
                        <input v-model="to" type="text" class="form-control text-center" placeholder="TO" aria-label="Arrival"
                            @input="searchto()" />
                    </div>
                    <p id="tocity"></p>
                    <div class="from-list" v-if="statusto" style="position: absolute; z-index: 1000" id="flightto-list" >
                       <table>
                          <tr v-for="(list, index) in flight_to_api"
                              :key="index"
                              style="cursor: pointer; background-color: whitesmoke">
                            <td scope="col" @click="setFlightTo(list)">
                              <b> {{ list[1] }}</b> ,<b>{{ list[2] }}</b> ,{{ list[0] }}
                            </td>
                          </tr>
                        </table>
                    </div>
            </div>
            <!-- DATE  -->
            <div class="col d-box text-center ">
                <br />
                <p class="text-muted"> Departing On &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Returning On </p> 
                <br />
                <HotelDatePicker  
                        @check-in-changed="checkInDate"
                        @check-out-changed="checkOutDate"
                        format="YYYY-MM-DD"
                >
                    
                </HotelDatePicker>
            </div>
            </div>
            <!-- for search -->
            <div class="row justify-content-center mt-2 mb-2">
                <a href="#" class="btn w-25" v-on:click="getFlight()">Find me a flight</a>
            </div>
            <!-- for weather -->
            <div class="row justify-content-center bg-light  mt-2 mb-2" id="weather_display" style="display: none">
                    <p id="city" style="text-align: center; color: #C70039 "></p>
            </div>

        <div class="row" id="weather_display1" style="display: none">
            <!-- card 1 -->
               <div class="col d-box text-center p-4">
                    <div class="card">
                        <div class="card-header">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-brightness-high"
                                viewBox="0 0 16 16">
                                <path
                                    d="M8 11a3 3 0 1 1 0-6 3 3 0 0 1 0 6zm0 1a4 4 0 1 0 0-8 4 4 0 0 0 0 8zM8 0a.5.5 0 0 1 .5.5v2a.5.5 0 0 1-1 0v-2A.5.5 0 0 1 8 0zm0 13a.5.5 0 0 1 .5.5v2a.5.5 0 0 1-1 0v-2A.5.5 0 0 1 8 13zm8-5a.5.5 0 0 1-.5.5h-2a.5.5 0 0 1 0-1h2a.5.5 0 0 1 .5.5zM3 8a.5.5 0 0 1-.5.5h-2a.5.5 0 0 1 0-1h2A.5.5 0 0 1 3 8zm10.657-5.657a.5.5 0 0 1 0 .707l-1.414 1.415a.5.5 0 1 1-.707-.708l1.414-1.414a.5.5 0 0 1 .707 0zm-9.193 9.193a.5.5 0 0 1 0 .707L3.05 13.657a.5.5 0 0 1-.707-.707l1.414-1.414a.5.5 0 0 1 .707 0zm9.193 2.121a.5.5 0 0 1-.707 0l-1.414-1.414a.5.5 0 0 1 .707-.707l1.414 1.414a.5.5 0 0 1 0 .707zM4.464 4.465a.5.5 0 0 1-.707 0L2.343 3.05a.5.5 0 1 1 .707-.707l1.414 1.414a.5.5 0 0 1 0 .708z" />
                            </svg>
                        </div>
                        <div class="card-body">
                            <p id="morning"></p>
                        </div>
                        <div class="card-footer">

                        </div>
                    </div>
                    
                 </div>
         
            <!-- card 2 -->
              <div class="col d-box text-center p-4">
                    <div class="card">
                        <div class="card-header">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-cloud-drizzle-fill"
                            viewBox="0 0 16 16">
                            <path
                                d="M4.158 12.025a.5.5 0 0 1 .316.633l-.5 1.5a.5.5 0 0 1-.948-.316l.5-1.5a.5.5 0 0 1 .632-.317zm6 0a.5.5 0 0 1 .316.633l-.5 1.5a.5.5 0 0 1-.948-.316l.5-1.5a.5.5 0 0 1 .632-.317zm-3.5 1.5a.5.5 0 0 1 .316.633l-.5 1.5a.5.5 0 0 1-.948-.316l.5-1.5a.5.5 0 0 1 .632-.317zm6 0a.5.5 0 0 1 .316.633l-.5 1.5a.5.5 0 1 1-.948-.316l.5-1.5a.5.5 0 0 1 .632-.317zm.747-8.498a5.001 5.001 0 0 0-9.499-1.004A3.5 3.5 0 1 0 3.5 11H13a3 3 0 0 0 .405-5.973z" />
                        </svg>
                        </div>
                        <div class="card-body">
                            <p id="afternoon"></p>
                        </div>
                        <div class="card-footer">

                        </div>
                    </div>
                    
                 </div>


            <!-- card 3 -->
              <div class="col d-box text-center p-4">
                    <div class="card">
                        <div class="card-header">
                           <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-thermometer-sun"
                                viewBox="0 0 16 16">
                                <path d="M5 12.5a1.5 1.5 0 1 1-2-1.415V2.5a.5.5 0 0 1 1 0v8.585A1.5 1.5 0 0 1 5 12.5z" />
                                <path
                                    d="M1 2.5a2.5 2.5 0 0 1 5 0v7.55a3.5 3.5 0 1 1-5 0V2.5zM3.5 1A1.5 1.5 0 0 0 2 2.5v7.987l-.167.15a2.5 2.5 0 1 0 3.333 0L5 10.486V2.5A1.5 1.5 0 0 0 3.5 1zm5 1a.5.5 0 0 1 .5.5v1a.5.5 0 0 1-1 0v-1a.5.5 0 0 1 .5-.5zm4.243 1.757a.5.5 0 0 1 0 .707l-.707.708a.5.5 0 1 1-.708-.708l.708-.707a.5.5 0 0 1 .707 0zM8 5.5a.5.5 0 0 1 .5-.5 3 3 0 1 1 0 6 .5.5 0 0 1 0-1 2 2 0 0 0 0-4 .5.5 0 0 1-.5-.5zM12.5 8a.5.5 0 0 1 .5-.5h1a.5.5 0 1 1 0 1h-1a.5.5 0 0 1-.5-.5zm-1.172 2.828a.5.5 0 0 1 .708 0l.707.708a.5.5 0 0 1-.707.707l-.708-.707a.5.5 0 0 1 0-.708zM8.5 12a.5.5 0 0 1 .5.5v1a.5.5 0 0 1-1 0v-1a.5.5 0 0 1 .5-.5z" />
                            </svg>
                        </div>
                        <div class="card-body">
                            <p id="evening"></p>
                        </div>
                        <div class="card-footer">

                        </div>
                    </div>
                    
                 </div>

            <!-- cars 4 -->
                 <div class="col d-box text-center p-4">
                    <div class="card">
                        <div class="card-header">
                           <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-moon-stars-fill"
                                viewBox="0 0 16 16">
                                <path
                                    d="M6 .278a.768.768 0 0 1 .08.858 7.208 7.208 0 0 0-.878 3.46c0 4.021 3.278 7.277 7.318 7.277.527 0 1.04-.055 1.533-.16a.787.787 0 0 1 .81.316.733.733 0 0 1-.031.893A8.349 8.349 0 0 1 8.344 16C3.734 16 0 12.286 0 7.71 0 4.266 2.114 1.312 5.124.06A.752.752 0 0 1 6 .278z" />
                                <path
                                    d="M10.794 3.148a.217.217 0 0 1 .412 0l.387 1.162c.173.518.579.924 1.097 1.097l1.162.387a.217.217 0 0 1 0 .412l-1.162.387a1.734 1.734 0 0 0-1.097 1.097l-.387 1.162a.217.217 0 0 1-.412 0l-.387-1.162A1.734 1.734 0 0 0 9.31 6.593l-1.162-.387a.217.217 0 0 1 0-.412l1.162-.387a1.734 1.734 0 0 0 1.097-1.097l.387-1.162zM13.863.099a.145.145 0 0 1 .274 0l.258.774c.115.346.386.617.732.732l.774.258a.145.145 0 0 1 0 .274l-.774.258a1.156 1.156 0 0 0-.732.732l-.258.774a.145.145 0 0 1-.274 0l-.258-.774a1.156 1.156 0 0 0-.732-.732l-.774-.258a.145.145 0 0 1 0-.274l.774-.258c.346-.115.617-.386.732-.732L13.863.1z" />
                            </svg>
                        </div>
                        <div class="card-body">
                            <p id="night"></p>
                        </div>
                        <div class="card-footer">

                        </div>
                    </div>
                    
                 </div>

         </div>
            <!-- for table to show available flights -->
           <div class="row d-box justify-content-center mt-2" id="display_flight" style="display: none">
            <h4 class="row  justify-content-center mt-4 ">
              Available Flight Information
            </h4>
           </div>
            <div class="row justify-content-center  mb-2" id="display_flight1" v-if="flight_info">

                <div class="col d-box text-center p-4">
                    <table style="width: 100% " class="flight_list_display" >
                        <tr>
                          <th>
                            Flight
                          </th>
                          <th>
                            Departure
                          </th>
                          <th>
                            Duration
                          </th>
                          <th>
                            Arrival
                          </th>
                          <th>
                            Price
                          </th>
                        </tr>
                        <tr v-for="user in users" :key="user.id">
                          <th> {{user. Flight}}</th>
                          <th>
                            {{user.Departure}}
                          </th>
                          <th>
                            {{user.Duration}}
                          </th>
                          <th>
                            {{user.Arrival}}
                          </th>
                          <th>
                            {{user.Price}}
                          </th>
                        </tr>
  
                      </table>

                    </div>
            </div>
    


    </div>

</template>

<script>
import axios from 'axios';
import HotelDatePicker from 'vue-hotel-datepicker'
import 'vue-hotel-datepicker/dist/vueHotelDatepicker.css';
import usersData from "./users.json";
export default {
  data () {
    return {
       users: usersData,
      statusfrom: null,
      statusto: null,
      flight_from_api: [],
      flight_to_api: [],
      from: null,
      to: null,
      destenation:null,
      flight_info:null,
      dates: {
        in: new Date().toISOString().slice(0, 10),
        out: new Date().toISOString().slice(0, 10),
      },

    
    }
  },
  methods:{
      checkInDate(val) {
      this.dates.in = val.toISOString().slice(0, 10);
      console.log(this.dates.in);
    },
    checkOutDate(val) {
      this.dates.out = val.toISOString().slice(0, 10);
      console.log(this.dates.out);
    },

    searchfrom() {
      this.statusfrom = true;
        axios

        .get(

        "https://api.sharetrip.net/api/v1/flight/search/airport?name=" +

        this.from

        )

        .then(res => {

        console.log(res.data);
        console.log(Object.values(res.data).length);
        //var responseData = Object.values(res.data);
        var responseData = null;
        var keys = Object.keys(res.data);
        for(var i in keys) {
          let index = keys[i];
          console.log(index);
          if(index === 'response') {
            responseData = res.data[index];
          }
        }
      
        console.log(keys);
        console.log(responseData);
        console.log(responseData[0].city);
         this.flight_from_api = [];
          for (let i = 0; i < responseData.length; i++) {
            this.flight_from_api[i] = [
              responseData[i].name,
              responseData[i].city,
              responseData[i].iata,
            ];
            console.log(this.flight_from_api)
          }



        
        })

        .catch(err => {

        console.log(err);

        });
},
    setFlightFrom(list) {
      this.from = list[2];
      document.getElementById("flightfrom-list").style.display = "none";
      document.getElementById(
        "fromcity"
      ).innerHTML = `${list[0]}<br><b>${list[1]}</b>`;
    },
    searchto() {
     this.statusto = true;
        axios

        .get(

        "https://api.sharetrip.net/api/v1/flight/search/airport?name=" +

        this.to

        )

        .then(res => {

        console.log(res.data);
        console.log(Object.values(res.data).length);
        //var responseData = Object.values(res.data);
        var responseData = null;
        var keys = Object.keys(res.data);
        for(var i in keys) {
          let index = keys[i];
          console.log(index);
          if(index === 'response') {
            responseData = res.data[index];
          }
        }
      
        console.log(keys);
        console.log(responseData);
        console.log(responseData[0].city);
         this.flight_from_api = [];
          for (let i = 0; i < responseData.length; i++) {
            this.flight_to_api[i] = [
              responseData[i].name,
              responseData[i].city,
              responseData[i].iata,
            ];
            console.log(this.flight_to_api)
          }



        
        })

        .catch(err => {

        console.log(err);

        });

    },
    setFlightTo(list) {

      this.to = list[2];
      this.destenation =list[1];
      document.getElementById("flightto-list").style.display = "none";
      document.getElementById(
        "tocity"
      ).innerHTML = `${list[0]}<br><b>${list[1]}</b>`;

    },
     getFlight() {
      document.getElementById("weather_display").style.display = "none";
      document.getElementById("weather_display1").style.display = "none";
      document.getElementById("display_flight").style.display = "none";
      this.flight_info=false;
      if (this.destenation.length > 0) {
      axios
                  .get(
                    "http://api.weatherapi.com/v1/forecast.json?key=fc00f9be98e04968a3535808213112&q=" +
                      this.destenation +
                      "&dt=2022-01-19" //weather api give me 14 days forcast data so I use fixed date otherwise I use this.date.to date for Forcast 
                  )
                  .then((response) => {
                    document.getElementById("weather_display").style.display = "flex";
                    document.getElementById("weather_display1").style.display = "flex";
                    document.getElementById("display_flight").style.display = "flex";
                    this.flight_info=true;
       document.getElementById(
              "city"
            ).innerHTML = `Weather For <b>${this.destenation}</b>`;
                    console.log(response.data);
                    var jsonObject = JSON.stringify(response.data);
                    // console.log(jsonObject);
                    var object = JSON.parse(jsonObject);
                    var forecast = object.forecast.forecastday;
                    
                    console.log(forecast);
                    console.log(Object.keys(object));
                    const countryfetch =object.location.country;
                    const cityfetch =object.location.name;
                    console.log(countryfetch);
                    console.log(cityfetch)
                  
                    const val1 = [];
                    const val2 = [];
                    const val3 = [];
                    const val4 = [];
                    // for farhinite vale
                    const far1 = [];
                    const far2 = [];
                    const far3 = [];
                    const far4 = [];
                   
                    for(var i =0; i<6; i++) {
                        console.log(forecast[0].hour[i].temp_c);
                        val1.push(forecast[0].hour[i].temp_c)
                      }
                      const sort1 = val1.sort();
                      console.log(sort1[0]);
                      console.log(sort1[sort1.length-1]); 
                      const low1 = Math.round(sort1[0]);
                      const high1 = Math.round(sort1[sort1.length-1]);
                    //  for farhinite
                    for(var i =0; i<6; i++) {
                      console.log(forecast[0].hour[i].temp_f);
                      far1.push(forecast[0].hour[i].temp_f)
                    }
                    const sortf1 = far1.sort();
                    console.log(sortf1[0]);
                    console.log(sortf1[sortf1.length-1]); 
                    const lowf1 = Math.round(sortf1[0]);
                    const highf1 = Math.round(sortf1[sortf1.length-1]);

                     document.getElementById(
                      "morning").innerHTML = `<b>MORNING</b><br><br><b>HIgh-${high1}℃ &nbsp&nbsp Low-${low1}℃ <br>HIgh-${highf1}°F &nbsp&nbsp Low-${lowf1}°F  </b>`;


                      // time 2
                    for(var i =6; i<12; i++) {
                        console.log(forecast[0].hour[i].temp_c);
                        val2.push(forecast[0].hour[i].temp_c)
                      }
                      const sort2 = val2.sort();
                      console.log(sort2[0]);
                      console.log(sort2[sort2.length-1]); 
                      const low2 = Math.round( sort2[0]);
                      const high2 = Math.round(sort2[sort2.length-1]);
                    //for ferhinite
                    for(var i =6; i<12; i++) {
                      console.log(forecast[0].hour[i].temp_f);
                      far2.push(forecast[0].hour[i].temp_f)
                    }
                    const sortf2 = far2.sort();
                    console.log(sortf2[0]);
                    console.log(sortf2[sortf2.length-1]); 
                    const lowf2 =Math.round( sortf2[0]);
                    const highf2 = Math.round(sortf2[sortf2.length-1]);
                    document.getElementById(
                    "afternoon").innerHTML = `<b>Afternoon</b><br><br><b>HIgh-${high2}℃ &nbsp&nbsp Low-${low2}℃ <br>HIgh-${highf2}°F &nbsp&nbsp Low-${lowf2}°F  </b>`;
                      // time 3 
                    for(var i =12; i<18; i++) {
                      console.log(forecast[0].hour[i].temp_c);
                      val3.push(forecast[0].hour[i].temp_c)
                      }
                      const sort3 = val3.sort();
                      console.log(sort3[0]);
                      console.log(sort3[sort3.length-1]); 
                      const low3 = Math.round(sort3[0]);
                      const high3 = Math.round(sort3[sort3.length-1]);
                      // for ferhinite
                    for(var i =12; i<18; i++) {
                        console.log(forecast[0].hour[i].temp_f);
                        far3.push(forecast[0].hour[i].temp_f)
                      }
                      const sortf3 = far3.sort();
                      console.log(sortf3[0]);
                      console.log(sortf3[sortf3.length-1]); 
                      const lowf3 = Math.round(sortf3[0]);
                      const highf3 = Math.round(sortf3[sortf3.length-1]);
                      document.getElementById(
                      "evening").innerHTML = `<b>Evening</b><br><br><b>HIgh-${high3}℃ &nbsp&nbsp Low-${low3}℃ <br>HIgh-${highf3}°F &nbsp&nbsp Low-${lowf3}°F  </b>`;
                      // time4
                    for(var i =18; i<24; i++) {
                      console.log(forecast[0].hour[i].temp_c);
                        val4.push(forecast[0].hour[i].temp_c)
                      }
                      const sort4 = val4.sort();
                      console.log(sort4[0]);
                      console.log(sort4[sort4.length-1]); 
                      const low4 = Math.round(sort4[0]);
                      const high4 = Math.round(sort4[sort4.length-1]);
                      // for farhinite
                      for(var i =18; i<24; i++) {
                        console.log(forecast[0].hour[i].temp_f);
                          far4.push(forecast[0].hour[i].temp_f)
                        }
                        const sortf4 = far4.sort();
                        console.log(sortf4[0]);
                        console.log(sortf4[sortf4.length-1]); 
                        const lowf4 = Math.round(sortf4[0]);
                        const highf4 = Math.round(sortf4[sortf4.length-1]);
                        document.getElementById(
                        "night").innerHTML = `<b>Night</b><br><br><b>HIgh-${high4}℃ &nbsp&nbsp Low-${low4}℃ <br>HIgh-${highf4}°F &nbsp&nbsp Low-${lowf4}°F  </b>`;
                  })
                  .catch((error) => {
                    console.log(error);
                  });
      }

     }

  },
  components: {
    HotelDatePicker,
  }
  };

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.d-box {
  background-color: #98B4D4;
  border-right: 6px solid  #A0DAA9;
}
.btn{
  background-color:  #88B04B;
}
table,
th,
tr,
td {
  border: 2px solid  grey;
  text-align: center;
}

</style>
