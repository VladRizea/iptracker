<template>
  <div class="container">
    <div class="header">
      <img class="background-image"  src="images/pattern-bg.png" alt="background pattern">

      <div class="top-section">
        
        <p class="title">IP adress tracker</p>
        <div class="ip-form">
          <form>
            <input class="ip-form-field" v-model="ip" placeholder="Search for any IP adress" type="text" onsubmit="" >
          </form>
          <div class="button" @click="updateIpStream()">
            <img src="images/icon-arrow.svg" alt=">">
          </div>
        </div>
    </div>
     <div class="middle-stats">
          <information-card title="IP ADRESS" :description="curentIp" ></information-card>
          <div class="divider"></div>
          <information-card title="LOCATION" :description="location" ></information-card>
          <div class="divider"></div>
          <information-card title="TIMEZONE" :description="timezone" ></information-card>
          <div class="divider"></div>
          <information-card title="ISP" :description="ISP" ></information-card>
        </div>
      </div>
    <div id="map"></div>
  </div>
</template>

<script>

import axios from 'axios';

import informationCard from "../components/information-card.vue"

export default {
components:{
        InformationCard: informationCard,
            },
  data() {
    
    return {
      ip: "",
      location: "-",
      timezone: "-",
      ISP: "-",
      lat: "",
      lng: "",
      mymap: "",
      marker: "",
      greenIcon : L.icon({iconUrl: 'images/icon-location.svg',iconSize:[46, 56],iconAnchor:[23, 56],}),
      curentIp: "",
    }
  },
  methods: {
    updateIpStream: async function()  {
      let response = axios.get("https://geo.ipify.org/api/v1?apiKey=at_FGUdTSSeCvlSHk4G26ik4Loyfyrea&ipAddress=" + this.ip)
      let data = await response;
      console.log(data);
      this.curentIp = data['data'].ip;
      this.location = data['data']['location'].city;
      this.timezone = "UTC"+ " " + data['data']['location'].timezone;
      this.ISP = data['data'].isp;
      this.lat = data['data']['location'].lat;
      this.lng = data['data']['location'].lng;


      this.marker = L.marker([this.lat, this.lng], {icon: this.greenIcon}).addTo(this.mymap);
      this.mymap.flyTo(new L.LatLng(this.lat, this.lng), 13);

      this.ip = "";

    }
  },
  mounted() {
     this.mymap = L.map('map' ,null, { zoomControl:false }).setView([45.94, 24.96], 13);
    L.tileLayer('https://api.maptiler.com/maps/basic/{z}/{x}/{y}.png?key=2SRn17LaW7QG7wlBX9dK', {
    attribution: '<a href="https://www.maptiler.com/copyright/" target="_blank">&copy; MapTiler</a> <a href="https://www.openstreetmap.org/copyright" target="_blank">&copy; OpenStreetMap contributors</a>',
    maxZoom: 18,
    zoomControl: false,
  }).addTo(this.mymap);
  this.mymap.zoomControl.remove();


  this.updateIpStream()
    

  },
}
</script>

<style lang="scss">

@import "../assets/flex";
@import "../assets/colors";
@import "../assets/screen-size";


.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
    .header{
      
      align-items: center;
      @include flexbox();
      @include justify-content(center);
        .background-image{
          align-self: center;
          background-size:cover;
          width: auto;
          height: 270px;
          position: fixed;
          overflow: hidden;
          top: 0;
        }
        .top-section{
          top: 0;
          position: absolute;
          align-items: center;
        .title{
          font-weight: 700;
          color: $cWhite;
          font-size: 35px;
          padding: 20px;
        }
        .ip-form{
          @include flexbox();
          @include flex-direction(row);
          @include justify-content(center);
            .button{
            align-items: center;
            @include flexbox();
            @include justify-content(center);
            height: 55px;
            width: 55px;
            background: $cBlack;
            border-radius: 0 15px 15px 0;
            background: $cBlack;
            transition: background 0.3s;
            &:hover{
              background: $cVeryDarkGray;
              cursor: pointer;
              transition: background 0.3s;
            }
            }
            .ip-form-field{
              height: 55px;
              @include lg{
                max-width: 450px;
                width: 33vw;}
              width: 70vw;
              border-radius: 15px 0 0 15px;
              font-size: 18px;
              font-weight: 400;
              padding: 0 12px;
              border:none;
              color: $cVeryDarkGray;
              &:focus{
                outline: none;
              }
            }
        }
        
        }

       .middle-stats{
         z-index: 99999;
          @include flexbox();
          @include lg{
          @include flex-direction(row);
          @include justify-content(space-around);
          width: 70vw;
          height: 150px;
          }
          @include flex-direction(column);
          @include justify-content(center);
          background: $cWhite;
          border-radius: 15px;
          width:calc(70vw + 55px);
          top: 195px;
          position: absolute;
          .divider{
            @include lg{
            display: block;
            }
            display: none;
            width: 1px;
            height: 70px;
            background: $cDarkGray;
            align-self: center;
          }
          }

    }
    
   #map{
          z-index: 1;
          position: absolute;
          height: calc(100vh - 270px);
          bottom: 0;
          left: 0;
          right: 0;
        }

}



</style>
