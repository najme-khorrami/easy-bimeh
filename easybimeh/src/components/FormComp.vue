<template>
    <section class="form-section q-my-xl">
        <div class="container">
            <div class="header row items-center">
                <h3 class="fs-lg q-pl-sm">یادآور تمدید بیمه نامه</h3>
            </div>
            <q-form @submit="onSubmit" greedy>
                <div class="row">
                    <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 q-pa-md">
                        <q-select outlined v-model="insureType" no-error-icon type="text" color="positive" :options="typeOptions" label="نوع بیمه نامه" hide-dropdown-icon behavior="menu" reactive-rules :rules="[ val => val !== null && val !== '' || 'نوع بیمه نامه']">
                            <template v-slot:prepend>
                                <q-avatar>
                                    <img src="../assets/insurance-type-rem.svg">
                                </q-avatar>
                            </template>
                        </q-select>
                    </div>
                    <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 q-pa-md">
                        <q-input outlined v-model="phone" type="tel" color="positive" label="شماره تلفن همراه">
                            <template v-slot:prepend>
                                <q-avatar>
                                    <img src="../assets/phone-rem.svg">
                                </q-avatar>
                            </template>
                        </q-input>
                    </div>
                    <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 q-pa-md">
                        <q-input outlined v-model="email" type="email" color="positive" label="ایمیل">
                            <template v-slot:prepend>
                                <q-avatar>
                                    <img src="../assets/email-rem.svg">
                                </q-avatar>
                            </template>
                        </q-input>
                    </div>
                    <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 q-pa-md">
                        <q-select outlined v-model="month" no-error-icon type="text" color="positive" :options="monthOptions" label="ماه" stack-label :dense="dense" hide-dropdown-icon behavior="menu" :rules="[ val => val !== null && val !== '' || 'ماه']">
                            <template v-slot:prepend>
                                <q-avatar>
                                    <img src="../assets/month-rem.svg">
                                </q-avatar>
                            </template>
                        </q-select>
                    </div>
                    <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 q-pa-md">
                        <q-select outlined filled="false" no-error-icon v-model="day" type="text" color="positive" :options="dayOptions" label="روز" stack-label :dense="dense" hide-dropdown-icon behavior="menu" :rules="[ val => val !== null && val !== '' || 'روز']">
                            <template v-slot:prepend>
                                <q-avatar>
                                    <img src="../assets/month-rem.svg">
                                </q-avatar>
                            </template>
                        </q-select>
                    </div>
                    <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 q-pa-md">
                        <q-input outlined v-model="name" type="text" color="positive" label="نام" :rules="[ val => val !== null && val !== '' || 'نام الزامی است']">
                            <template v-slot:prepend>
                                <q-avatar>
                                    <img src="../assets/person-rem.svg">
                                </q-avatar>
                            </template>
                        </q-input>
                    </div>
                    <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 q-pa-md">
                        <q-input outlined v-model="family" type="text" color="positive" label="نام خانوادگی بیمه گذار">
                            <template v-slot:prepend>
                                <q-avatar>
                                    <img src="../assets/person-rem.svg">
                                </q-avatar>
                            </template>
                        </q-input>
                    </div>
                    <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 q-pa-md">
                        <q-select outlined v-model="state" no-error-icon type="text" color="positive" :options="stateOptions" label="استان" stack-label :dense="dense" hide-dropdown-icon behavior="menu" :rules="[ val => val !== null && val !== '' || 'استان']">
                            <template v-slot:prepend>
                                <q-avatar>
                                    <img src="../assets/location-rem.svg">
                                </q-avatar>
                            </template>
                        </q-select>
                    </div>
                    <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 q-pa-md">
                        <q-select outlined v-model="city" no-error-icon type="text" color="positive" label="شهر" stack-label :dense="dense" hide-dropdown-icon behavior="menu" >
                            <template v-slot:prepend>
                                <q-avatar>
                                    <img src="../assets/location-rem.svg">
                                </q-avatar>
                            </template>
                        </q-select>
                    </div>
                    <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12 q-pa-md">
                        <q-btn label="یادآوری کن" type="submit" class="bg-red-5 text-white q-pa-md"></q-btn>
                    </div>
                </div>
            </q-form>
        </div>
    </section>
</template>
  
<script>
  import { defineComponent,ref } from 'vue'
  import axios from 'axios'

  export default defineComponent({
    name: 'FormComp',
    setup() {
        const insureType = ref(null)
        const phone = ref(null)
        const email = ref(null)
        const month = ref(null)
        const day = ref(null)
        const name = ref(null)
        const family = ref(null)
        const state = ref(null)
        const city = ref(null)

      return {
        model: ref(null),
        typeOptions: ['بیمه ثالث خودرو', 'بیمه بدنه', 'بیمه آتش سوزی', 'بیمه درمان مسافرتی', 'بیمه آسانسور','سایر بیمه نامه ها'],
        monthOptions: ['فروردین','اردیبهشت','خرداد','تیر','مرداد','شهریور','مهر','آبان','آذر','ذی','بهمن','اسفند'],
        dayOptions: ['1ام','2ام','3ام','4ام','5ام','6ام','7ام','8ام','9ام','10ام','11ام','12ام','13ام','14ام','15ام','16ام','17ام','18ام','19ام','20ام','21ام','22ام','23ام','24ام','25ام','26ام','27ام','28ام','29ام','30ام','31ام',],
        stateOptions: ['آذربایجان','البرز','ایلام','بوشهر','تهران','سمنان','فارس','قزوین','گیلان'],
        dense: ref(false),
        insureType, phone, email, month, day, name, family, state, city,
        onSubmit () {
            axios.post('https://jsonplaceholder.typicode.com/users', {
                title: insureType,
                phoneNumber: phone,
                email: email,
                month: month,
                day: day,
                name: name,
                familyName: family,
                province: state,
                city: city
            })
            .then(function (response) {
                console.log(response);
            })
            .catch(function (error) {
                console.error(error);
            });
        }
      }
    }
  })
</script>
  
<style lang="scss" scoped>
    .q-btn {
        width: 70%;
    }
    .q-avatar {
        display: block !important;
    }
    @media (max-width: $breakpoint-sm-min) {
        .header h3 {
           font-size: 16px;
        }
    }
</style>