<template>

    <section class="companies-section q-my-xl">
        <div class="container">
            <div class="header text-center">
                <h3 class="fs-lg q-pl-sm">شرکت های بیمه</h3>
            </div>
            <div class="box-container row justify-center">
                <q-card v-for="item in insureCompany" :key="item.title" class="q-ma-sm q-pa-sm shadow-4">
                    <img :src="item.metaMediaLogoFileUrl" />
                </q-card>
            </div>
        </div>
    </section>

</template>
  
<script>
  import { defineComponent } from 'vue'
  import axios from 'axios'

  export default defineComponent({
    name: 'SlidersComp',
    setup() {

      const insureCompany = []
      axios.get('https://server.easybimeh.com/api/Information?key=0', {
        params: {_limit: 10}
      })
      .then(function (response) {       
        for(let i=1 ; i<11 ; i++) {
          insureCompany.push(response.data.message.insuranceCompany[i])
        }
      })
      .catch(function (error) {
        console.error(error);
      });

      return {
        insureCompany
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