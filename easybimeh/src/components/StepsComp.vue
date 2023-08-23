<template>

    <section class="steps-section q-mt-xl">
        <div class="container">
            <div class="header row justify-center items-center">
                <q-img src="../../src/assets/steps-icon.svg" width="48px" height="60px"></q-img>
                <h3 class="fs-lg q-pl-sm"> فقط با چند کلیک خودت رو بیمه کن!</h3>
            </div>
            <div class="bg-instead q-px-md">
                <q-img src="../assets/mobile-banner.png"></q-img>
            </div>
            <div class="box-container row no-wrap justify-evenly relative-position">
                <div class="step-item shadow-15 q-ma-md q-pa-lg column justify-center items-center no-wrap" v-for="item in stepsList" :key="item.id"  :id="item.id" @mouseover="runProgress">
                    <q-img :src="item.src" fit="contain"  :id="item.id"></q-img>
                    <span class="fs-sm text-center q-pt-md" :id="item.id">{{ item.title }}</span>
                </div> 
            </div>
            <div class="q-pa-xl">
                <q-linear-progress :value="progress" rounded color="orange" class="q-mt-lg" />
            </div>
        </div>
    </section>

    <section class="intro-slider-section q-mt-xl">
        <div class="container">
            <div class="header row justify-center items-center">
                <q-img src="../../src/assets/insurance-policies.svg" fit="contain" width="48px" height="60px"></q-img>
                <h3 class="fs-lg q-pl-sm">معرفی بیمه نامه ها</h3>
            </div>

            <!-- slider -->
            <carousel items-to-show="1" wrapAround="true" autoplay="3000" transition="500" dir="rtl" :breakpoints="breakpoints" pauseAutoplayOnHover="true">
                <Slide v-for="item in introList" :key="item.title">
                    <div class="carousel__item">
                        <q-card class="my-card q-my-md q-pa-md relative-position shadow-3" style="height: 500px;">
                            <q-img :src="'https://media.easybimeh.com//Easybimeh/' + item.imagePath" :img-style="{ borderRadius: '10px' }"></q-img>
                            <q-card-section class="text-center q-mt-md">
                                <div class="text-h6">{{ item.title }}</div>
                                <div class="text-subtitle2 description">{{ item.description }}</div>
                            </q-card-section>
                            <q-card-section class="footer-card q-pt-none row justify-between items-center absolute-bottom q-pt-md" tag="a">
                                <span>شرایط بیمه نامه</span>
                                <span class="fs-lg">&#8592;</span>
                            </q-card-section>
                        </q-card>
                    </div>
                </Slide>
            </carousel>
            <!-- slider -->
            
        </div>
    </section>

</template>
  
<script>
  import { defineComponent,ref } from 'vue'
  import axios from 'axios'
  import 'vue3-carousel/dist/carousel.css'
  import { Carousel, Slide } from 'vue3-carousel'

  export default defineComponent({
    name: 'StepsComp',
        components: {
        Carousel,
        Slide,
    },
    setup() {
        const progress = ref(0)
        const introList = []
        axios.get('https://server.easybimeh.com/api/Information?key=0', {
            params:{_limit: 6}
        })
        .then(function (response) {       
            for(let i=0 ; i<6 ; i++) {
                introList.push(response.data.message.insuranceType[i])
            }
        })
        .catch(function (error) {
            console.error(error);
        });
        const stepsList = [
            {id:1 ,title:'بیمه مورد نظرت رو انتخاب کن' ,src:'./src/assets/step1.svg'},
            {id:2 ,title:'مشخصات مورد بیمه رو وارد کن' ,src:'./src/assets/step2.svg'},
            {id:3 ,title:'قیمت بیمه رو استعلام کن' ,src:'./src/assets/step3.svg'},
            {id:4 ,title:'درخواستت رو نهایی کن' ,src:'./src/assets/step4.svg'},
            {id:5 ,title:'بیمه نامه  ات آماده است' ,src:'./src/assets/step5.svg'},
        ]
      return {
        stepsList,
        introList,
        progress,
        runProgress (e) {
            progress.value = e.target.id / 5 - .1
        },
        breakpoints: {
            600: {
                itemsToShow: 2,
            },
            1200: {
                itemsToShow: 3,
            },
        }
      }
    }
  })
</script>
  
<style lang="scss" scoped>
    .step-item {
        background-color: #ccdbda;
        width: 200px;
        height: 200px;
        border-radius: 20px;
        overflow: hidden;
        transition: .5s;
    }
    .my-card {
        & .q-img {
            height: 100%;
            max-height: 200px;
        }
    }
    .description {
        height: 90px;
        overflow: hidden;
        text-overflow: ellipsis; 
    }
    .footer-card {
        border-top: 1px solid $grey-5;
    }
    .step {
        z-index: 2;
    }
    .bg-instead {
        display: none;
    }
    // slider
    .carousel__item {
        width: 100%;
    }
    .carousel__slide {
        padding: 10px;
    }
    @media (max-width: $breakpoint-sm-min) {
        .header h3 {
           font-size: 16px;
        }
    }
    @media (max-width: $breakpoint-sm-max) {
        .steps-section {
            & .box-container {
                display: none;
            }
            & .q-linear-progress {
                display: none;
            }
            & .bg-instead {
                display: block;
            }
        }
    }
</style>