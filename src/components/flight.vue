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
                            @input="srchfrom()" />
                    </div>
                    <p id="fromcity"></p>
                    <div class="from-list" v-if="status_flight_from" style="position: absolute; z-index: 1000"
                        id="flightfrom-code-list">
                        <table>
                            <tr>
                                <td>
                                    
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
                            @input="srchto()" />
                    </div>
                    <p id="tocity"></p>
                    <div class="from-list" v-if="status_flight_to" style="position: absolute; z-index: 1000" id="flightto-code-list">
                        <tr >
                            <td >
                            
                            </td>
                        </tr>
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
                <a href="#" class="btn btn-info w-25" v-on:click="getFlight()">Find me a flight</a>
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
export default {
  data () {
    return {
      status_flight_from: null,
      status_flight_to: null,
      flight_code_from: [],
      flight_code_to: [],
      depdate: null,
      arrdate: null,
      from: null,
      to: null,
      //flight display
      pick: "Pick a Date",
      states: {
        disabledDates: {
          to: new Date(Date.now() - 86400000),
        },
      },
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.d-box {
  background-color: whitesmoke;
  border-right: 6px solid darkcyan;
}
</style>
