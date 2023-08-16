<template>
  <q-layout view="lHh Lpr lFf">

    <q-header elevated class="bg-primary">
      <div class="container">
        <q-toolbar class="q-ma-xs">
          <q-toolbar-title class="fs">{{ title }}</q-toolbar-title>
          <q-space />
          <q-btn color="green-7 q-mr-sm" label="ورود"/>
          <q-btn color="green-4" label="ثبت نام"/>
          <q-avatar size="50px" square @click="showMenu">
            <q-btn icon="menu" size="20px"></q-btn>
          </q-avatar>
        </q-toolbar>
      </div>
      <div class="container">
        <q-tabs align="left" class="q-ma-xs">
          <q-route-tab to="" v-for="item in tabList" :key="item" :label="item" />
        </q-tabs>
      </div>
    </q-header>

    <!--menu-content-->
    <!-- <div class="menu">

    </div> -->

    <q-page-container>
      <router-view />
    </q-page-container>

    <div class="footer-1 bg-grey-5 text-dark q-pa-md">
      <q-toolbar>
        <div class="container full-width">
          <div class="row full-width justify-start">
            <div class="col-12 col-sm-6 column">
              <h6 class="q-my-xs">امکانات سایت</h6>
              <ul>
                <li v-for="item in footerList" :key="item" class="q-py-xs">
                  <a href="#">{{ item }}</a>
                </li>
              </ul>
            </div>
            <div class="col-12 col-sm-6 column ">
              <h6 class="q-my-xs q-mb-md">ارتباط با ما</h6>
              <div v-for="item in footerConct" :key="item.title" class="row items-center q-py-xs">
                <img :src="item.src" alt="">
                <span class="q-ml-sm">{{ item.title }}</span>
              </div>
            </div>
          </div>
        </div>
      </q-toolbar>
    </div>

    <div class="footer-2 bg-grey-4 text-dark q-pa-md">
      <q-toolbar>
        <div class="container full-width">
          <div class="row no-wrap full-width justify-center">
            <div class="img-footer">
              <q-img src="../assets/footer-icon.png" fit="contain"></q-img>
            </div>
            <div class="img-footer">
              <q-img src="../assets/samandehi.png" fit="contain"></q-img>
            </div>
          </div>
        </div>
      </q-toolbar>
    </div>

  </q-layout>
</template>

<script>
import { defineComponent} from 'vue'

export default defineComponent({
  name: 'MainLayout',

  setup () {
    const title = 'کارگزاری راه سبز توسعه امید'
    const tabList = ['خانه','محصولات و خدمات','مجله بیمه ای','پیگیری','درباره ما','تماس با ما']
    const footerList = ['درباره ما','خدمات ما','تماس با ما','پیشنهادات ، انتقادات و شکایات','پرسش های متداول','پیگیری درخواست','قوانین و مقررات']
    const footerConct = [
      {title:'aka.co.ir@gmail.com' ,src:'https://img.icons8.com/pulsar-color/30/000000/secured-letter.png'},
      {title:'02191691049' ,src:'https://img.icons8.com/pulsar-color/30/8EE8D7/phone.png'},
      {title:'آدرس : تهران خ میرداماد ساختمان نقره' ,src:'https://img.icons8.com/pulsar-color/30/8EE8D7/place-marker.png'}
    ]

    return {
      title,
      tabList,
      footerList,
      footerConct,
      showMenu() {

      }
    }
  }
})
</script>

<style lang="scss">
  a {
    text-decoration: none;
    color: $dark;
  }
  .footer-2 .q-img {
    width: 150px;
    height: 150px;
  }
  @media (max-width: $breakpoint-md-min) {
    .q-toolbar > .q-btn {
      display: none;
    }
    .q-header .q-tabs {
      display: none;
    }
    .q-space {
      display: none;
    }
  }
  @media (min-width: $breakpoint-md-min) {
    .q-avatar {
      display: none !important;
    }
  }
  @media (max-width: $breakpoint-sm-min) {
        .footer-1 h6 {
           font-size: 16px;
        }
    }
</style>