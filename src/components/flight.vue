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
                    <div class="from-list" v-if="statusto" style="position: absolute; z-index: 1000" id="flightto-list">
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
            <div class="col d-box text-center">
                <br />
                <span class="text-muted"> Departing On </span>
                <Datepicker v-model="depdate" class="text-center" :disabled-dates="states.disabledDates" :placeholder="pick">
                </Datepicker>
                <hr class="my-4" />
                <span class="text-muted"> Returning On </span>
                <Datepicker v-model="arrdate" class="text-center mb-4" :disabled-dates="states.disabledDates" :placeholder="pick">
                </Datepicker>
            </div>
            </div>
            <!-- for search -->
            <div class="row justify-content-center mt-2 mb-2">
                <a href="#" class="btn w-25" v-on:click="getFlight()">Find me a flight</a>
            </div>
            <!-- for weather -->
            <div class="row justify-content-center bg-light  mt-2 mb-2">
                    <p id="" style="text-align: center;"> Weather from </p>
            </div>

        <div class="row">
            <!-- card 1 -->
           
                <div class="col d-box text-center p-4">
                    <p id="weather_morning"></p>
                </div>
         
            <!-- card 2 -->
                <div class="col d-box text-center p-4">
                    <p id="weather_afternoon"></p>
                </div>
            <!-- card 3 -->
                <div class="col d-box text-center p-4">
                    <p id="weather_evening"></p>
                </div>
            <!-- cars 4 -->
                <div class="col d-box text-center p-4">
                        <p id="weather_overnight"></p>
                </div>
         </div>

    


    </div>

</template>

<script>
import axios from 'axios';
export default {
  data () {
    return {
      statusfrom: null,
      statusto: null,
      flight_from_api: [],
      flight_to_api: [],
      depdate: null,
      arrdate: null,
      from: null,
      to: null,
      pick: "Pick a Date",
      states: {
        disabledDates: {
          
        },
      },
    }
  },
  methods:{
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
      document.getElementById("flightto-list").style.display = "none";
      document.getElementById(
        "tocity"
      ).innerHTML = `${list[0]}<br><b>${list[1]}</b>`;

    }

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
</style>
