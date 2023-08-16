<template>
    
    <div class="main-page container">
        <div class="row">
            <div class="col-12 col-md-6 q-pa-xl">
                <q-carousel swipeable animated v-model="slide" autoplay transition-prev="slide-left" transition-next="slide-right" ref="carousel" infinite>
                    <q-carousel-slide :name="1" img-src="../../src/assets/bikary.jpg">
                        <div class="slide-content row justify-between absolute-bottom text-white q-pl-md items-center">
                            <span>بیمه بیکاری</span>
                            <q-btn flat class="fs-lg">&#8592;</q-btn>
                        </div>
                    </q-carousel-slide>
                    <q-carousel-slide :name="2" img-src="../../src/assets/bikary.jpg">
                        <div class="slide-content row justify-between absolute-bottom text-white q-pl-md items-center">
                            <span>بیمه بیکاری</span>
                            <q-btn flat class="fs-lg">&#8592;</q-btn>
                        </div>
                    </q-carousel-slide>
                </q-carousel>
            </div>
            <div class="col-12 col-md-6 column justify-center items-center">
                <h2 class="fs-lg text-weight-bold q-ma-nonete text-white">ارائه دهنده خدمات نوین بیمه آنلاین</h2>
                <h3 class="fs-md q-mt-none text-white">ساعات کاری از ساعت 8 صبح تا 5 عصر</h3>
                <q-btn-group class="banner-button justify-between">
                    <img src="../assets/download.svg" class="q-ma-sm" alt="">
                    <q-btn color="transparent" rounded class="fs-md" label="طرح های ویژه" />
                    <q-btn color="transparent" rounded label="&#8592;" class="arrow fs-lg" />
                </q-btn-group>
            </div>
        </div>
    </div>

    <InsuranceBox />
    <StepsComp />
    <FormComp />
    <SlidersComp />
    
</template>

<script>
import { defineComponent,ref } from 'vue'
import InsuranceBox from 'components/InsuranceBox.vue';
import StepsComp from 'components/StepsComp.vue';
import FormComp from 'components/FormComp.vue';
import SlidersComp from 'components/SlidersComp.vue';

export default defineComponent({
  name: 'mainPage',
  
  components: {
    InsuranceBox,
    StepsComp,
    FormComp,
    SlidersComp
  },

  setup () {
    return {
      slide: ref(1)
    }
  }
})
</script>
<style lang="scss" scoped>
    .main-page {
        background-color: $primary;
        border-radius: 0% 25% 50% 48%/25% 0% 8% 9%;
        padding-bottom: 100px;
    }
    .slide-content {
        background: linear-gradient(99.41deg,darken($primary,7%),rgba(darken($primary,7%),.6));
    }
    .q-carousel {
        border-radius: 10px;
        overflow: hidden;
        max-width: 550px;
        max-height: 320px;
    }
    .banner-button {
        background: linear-gradient(99.41deg,#ff006a,#face3c);
        width: 300px;
        height: 70px;
    }
    .q-btn-group {
        border-radius: 50px;
    }
    @media (max-width: $breakpoint-md-min) {
        .row > div .q-carousel{
            margin: auto;
        }
    }
</style>