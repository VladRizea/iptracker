<template>
  <div class="container">
    <div class="header">
      <img class="background-image" src="images/pattern-bg.png" alt="background pattern">

      <div class="top-section">
        <p class="title">IP adress tracker</p>
        <div class="ip-form">
          <form>
            <input class="ip-form-field" v-model="ip"  placeholder="Search for any IP adress" type="text" onsubmit="" >
          </form>
          <div class="button">
            <img src="images/icon-arrow.svg" alt=">">
          </div>
        </div>

        <div style="height: 59px"></div>

        <div class="middle-stats">
          <information-card title="IP ADRESS" description="191.212.174.333" ></information-card>
          <div class="divider"></div>
          <information-card title="LOCATION" description="Brooklin, NY 10001" ></information-card>
          <div class="divider"></div>
          <information-card title="TIMEZONE" description="UTC: -05:00" ></information-card>
          <div class="divider"></div>
          <information-card title="ISP" description="Spacex Starlink" ></information-card>
        </div>
      </div>

      
      
    </div>
    
  </div>
</template>

<script>
import informationCard from "../components/information-card.vue"
export default {
components:{
        InformationCard: informationCard,
            },
  data() {
    
    return {
      ip: "",
    }
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
                width: 33vw;
              }
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
        .middle-stats{
          @include flexbox();
          
          @include lg{
          @include flex-direction(row);
          @include justify-content(space-around);
          width: 70vw;
          height: 150px;
          }
          @include flex-direction(column);
          @include justify-content(space-around);
          background: $cWhite;
          border-radius: 15px;
          
          width: 80vw;
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

    }
    
}



</style>
