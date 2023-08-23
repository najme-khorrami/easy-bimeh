<template>
  <div class="container">
    <div class="box-container row justify-center relative-position">
      <a class="insurance-item shadow-15 q-ma-sm q-pa-lg column justify-center items-center no-wrap bg-white" v-for="item in insurList" :key="item.id" >
        <q-img :src="'https://media.easybimeh.com//Easybimeh/' + item.iconImagePath" fit="contain"></q-img>
        <span class="fs-sm text-center q-pt-md">{{ item.title }}</span>
      </a> 
    </div>
    <q-separator spaced="50px" />
    <div class="row justify-center relative-position">
      <a class="plans-item q-ma-sm q-pa-lg column justify-center items-center no-wrap" v-for="item in plansList" :key="item.id" :href="item.src">
        <q-img :src="item.img" fit="contain"></q-img>
        <span class="fs-sm text-center q-pt-md">{{ item.title }}</span>
      </a> 
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue'
import axios from 'axios'

export default defineComponent({
  name: 'InsuranceBox',
  setup() {
    const insurList = []
    axios.get('https://server.easybimeh.com/api/Information?key=0', {
      params: {_limit: 6 }
    })
    .then(function (response) {       
        for(let i=0 ; i<6 ; i++) {
          insurList.push(response.data.message.insuranceType[i])
          // console.log(response.data.message.insuranceType[i])
        }
      })
      .catch(function (error) {
        console.error(error);
      });

    const plansList = [
      {title:'طرح های بیمه درمان خانواده' ,src:'#' ,img:'./src/assets/family-insure.png'},
      {title:'طرح های بیمه آتش سوزی منازل مسکونی ' ,src:'#' ,img:'./src/assets/fire-insure.png'},
      {title:'طرح های بیمه آسانسور ' ,src:'#' ,img:'./src/assets/elevator-insure.png'},
      {title:'طرح های بیمه درمان انفرادی' ,src:'#' ,img:'./src/assets/person-insure.png'}
    ]
    return {
      insurList,
      plansList
    }
  }
})
</script>

<style lang="scss" scoped>
  .box-container {
    top: -100px;
    margin-bottom: -100px;
  }
  .insurance-item {
    width: 154px;
    height: 170px;
    border-radius: 20px;
    overflow: hidden;
    transition: .5s;
    &:hover {
      transform: translateY(-5px);
    }
  }
  a {
    cursor: pointer;
  }
  .q-separator {
    width: 100%;
    max-width: 75%;
    margin: auto;
  }
  .plans-item {
    width: 154px;
    height: 170px;
    border-radius: 20px;
    overflow: hidden;
    border: 2px solid lighten($primary, 15%);
    &:hover {
      background-color: $grey-3;
    }
  }
  @media (max-width: $breakpoint-md-min) {
    .box-container {
      top: -50px;
      margin-bottom: -50px;
    }
  }
</style>