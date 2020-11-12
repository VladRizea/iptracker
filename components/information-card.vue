<template>
  <div class="wrapper-information">
      <p class="title-style">{{title}}</p>
      <p class="info-style">{{description}}</p>
  </div>
</template>

<script>
export default {
    props: [
        'title',
        'description',
    ]
}
</script>

<style lang="scss">

@import "../assets/flex";
@import "../assets/colors";
@import "../assets/screen-size";

.wrapper-information{
    @include flexbox();
    justify-self: center;
    @include lg{
        @include justify-content(flex-start);
        @include flex-direction(column); 
        text-align: left;
        align-items: flex-start;
        padding: 35px 0 0 0;
        width: 12vw;
        height: 150px;
    }
    @include justify-content(center);
    @include flex-direction(column); 
    text-align: center;
    align-items: center;
    align-self: center;
    width:calc(70vw + 55px);
    height: 70px;
    padding: 0 0 0 0;
    .title-style{       
        color: $cDarkGray;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: 700;
    }
    .info-style{
         @include lg{
            font-size: 1.6vw;
        }
        padding: 5px 0 0 0;
        color: $cVeryDarkGray;
        font-size: 4vw;
    }
}
</style>