<template>

    <section class="companies-section q-my-xl">
        <div class="container">
            <div class="header text-center">
                <h3 class="fs-lg q-pl-sm">شرکت های بیمه</h3>
            </div>
            <!-- slider -->
            <Carousel items-to-show="3" wrapAround="true" autoplay="3000" dir="rtl" transition="500" :breakpoints="coBreakpoints" pauseAutoplayOnHover="true">
              <Slide v-for="item in insureCompany" :key="item.title">
                <div class="carousel__item">
                  <q-card class="q-my-sm q-pa-sm shadow-4">
                    <img :src="item.metaMediaLogoFileUrl" />
                  </q-card>
                </div>
              </Slide>
            </Carousel>
            <!-- slider -->
        </div>
    </section>

</template>
  
<script>
  import { defineComponent } from 'vue'
  import axios from 'axios'
  import 'vue3-carousel/dist/carousel.css'
  import { Carousel, Slide  } from 'vue3-carousel'

  export default defineComponent({
    name: 'SlidersComp',
    components: {
      Carousel,
      Slide
    },
    setup() {

      const insureCompany = []
      axios.get('https://server.easybimeh.com/api/Information?key=0', {
        params: {_limit: 14}
      })
      .then(function (response) {       
        for(let i=1 ; i<15 ; i++) {
          insureCompany.push(response.data.message.insuranceCompany[i]) 
        }
      })
      .catch(function (error) {
        console.error(error);
      });

      return {
        insureCompany,
        coBreakpoints: {
          580: {
            itemsToShow: 4,
          },
          790: {
            itemsToShow: 6,
          },
          1200: {
            itemsToShow: 8,
          },
          1200: {
            itemsToShow: 10,
          },
        }
      }
    }
  })
</script>
  
<style lang="scss" scoped>
  .companies-section .q-card {
    width: 100%;
    max-width: 100px;
  }
  @media (max-width: $breakpoint-sm-min) {
        .header h3 {
           font-size: 16px;
        }
    }
</style>