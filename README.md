<h1 align="center">Welcome to flight-booking 👋</h1>
<p>
  <img alt="Version" src="https://img.shields.io/badge/version-1.0.0-blue.svg?cacheSeconds=2592000" />
  <img src="https://img.shields.io/badge/node-%3E%3D%2014.0.0-blue.svg" />
  <img src="https://img.shields.io/badge/npm-%3E%3D%203.0.0-blue.svg" />
</p>

# A flight-booking Interface using Vue js

This is 
basically a flight booking interface for the  user.


## Features

- User can easily find the airport information.
- User can select date for travel  
- User can know about the destination Weather Forcast
- User can see available Flight information(demo jeson file)
- 


## Prerequisites

- node >= 14.0.0
- npm >= 3.0.0

## Installation

Install my-project with npm

```bash
  npm install 
  npm install -g @vue/cli
  npm update -g @vue/cli
  npm install -g @vue/cli-init
  vue intit webpack projectname
  npm install --save axios vue-axios
  npm install vue-hotel-datepicker 
  npm run dev

```
    
## API Reference

#### WeatherAPI.com

```http
  https://rapidapi.com/weatherapi/api/weatherapi-com/
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `api_key` | `string` | **Required**. Your API key |



###### API code Format
```http
    var axios = require("axios").default;
    var options = {
    method: 'GET',
    url: 'https://weatherapi-com.p.rapidapi.com/forecast.json',
    params: {q: 'London', days: '3'},
    headers: {
    'x-rapidapi-host': 'weatherapi-com.p.rapidapi.com',
    'x-rapidapi-key': '3c2ec3f5bemshb153f76bc5858a4p131b0djsna6224901994f'
    }
    };

axios.request(options).then(function (response) {
	console.log(response.data);
}).catch(function (error) {
	console.error(error);
});
```
#### sharetrip.net

```http
  "https://api.sharetrip.net/api/v1/flight/search/airport?name="
```

###### API code Format
```http
 axios

        .get(

        "https://api.sharetrip.net/api/v1/flight/search/airport?name=" +

        this.to

        )

        .then(res => {
        )}.catch(function (error) {
	    console.error(error);
        });

```



## Lessons Learned

I learn besic concept about Vue js. How vue js works and how components,props emmits work.In This project we also use api so I learn how to fetch data from api and how to show autocomplete from api.I also learn vue js date picker and how to read json file in vue js.   


## Screenshots

![App Screenshot](https://i.ibb.co/PZRz6G7/Screenshot-from-2022-01-05-17-21-18.png)
![App Screenshot](https://i.ibb.co/6tsnYwy/Screenshot-from-2022-01-05-17-21-29.png)
![App Screenshot](https://i.ibb.co/rywMX5y/Screenshot-from-2022-01-05-17-21-59.png)
![App Screenshot](https://i.ibb.co/fYnkwJ2/Screenshot-from-2022-01-05-17-22-05.png)
## Tech Stack

**Server:** Vue js,javascript,Html,Css,Bootstrap




## Feedback

If you have any feedback, please reach out to us at tanvir@w3engineers.com


## 🚀 About Me
I'm a Softwere Engineer Intern...
