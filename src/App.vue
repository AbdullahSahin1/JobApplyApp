<template>
  <div class="h-screen w-full p-20 flex gap-8">
    <div class="p-6 rounded-md shadow-lg bg-white w-1/2 border border-solid border-gray-600">

      <DynamicInput />
<!--      <form @submit.prevent="submitMyForm">
        <div class="mb-4 flex flex-col">
          <label for="nameInput" class="text-gray-500 text-xs mb-2">Ad</label>
          <input id="nameInput" v-model="user.name"
                 :class="userValidations.name?'isError':''"
                 class="block w-full font-normal text-base
            text-gray-700 bg-white rounded border border-solid border-gray-400
            transition ease-in outline-none
            px-3 py-1 m-0 focus:text-gray-900
            focus:border-blue-600 placeholder-gray-400 placeholder:text-xs"
                 placeholder="John"
          >
        </div>
        <div class="mb-4 flex flex-col">
          <label for="surnameInput" class="text-gray-500 text-xs mb-2">Soyad</label>
          <input id="surnameInput"
                 v-model="user.surname"
                 :class="userValidations.surname?'isError':''"
                 class="block w-full font-normal text-base
            text-gray-700 bg-white rounded border border-solid border-gray-400
            transition ease-in outline-none
            px-3 py-1 m-0 focus:text-gray-900
            focus:border-blue-600 placeholder-gray-400 placeholder:text-xs"
                 placeholder="Doe"
          >
        </div>
        <div class="mb-4 flex flex-col">
          <label for="emailInput" class="text-gray-500 text-xs mb-2">Email</label>
          <input id="emailInput" type="email"
                 v-model="user.email"
                 :class="userValidations.email?'isError':''"
                 class="block w-full font-normal text-base
            text-gray-700 bg-white rounded border border-solid border-gray-400
            transition ease-in outline-none
            px-3 py-1 m-0 focus:text-gray-900
            focus:border-blue-600 placeholder-gray-400 placeholder:text-xs"
                 placeholder="abc@mail.com"
          >
        </div>
        <div class="mb-4 flex flex-col">
          <label for="countryInput" class="text-gray-500 text-xs mb-2">Ülke</label>
          <select id="countryInput" v-model="user.country" class="block w-full font-normal text-base
            text-gray-700 bg-white rounded border border-solid border-gray-400
            transition ease-in outline-none
            px-3 py-1 m-0 focus:text-gray-900
            focus:border-blue-600 placeholder-gray-400 placeholder:text-xs">
            <option v-for="item in getCountries" :key="item.id" :value="item.id">{{ item.name }}</option>

          </select>
        </div>

        <div class="mb-4 flex flex-col">
          <label for="adressInput" class="text-gray-500 text-xs mb-2">Adres</label>
          <textarea v-model="user.adress" id="adressInput"
                    :class="userValidations.adress?'isError':''"
                    class="block w-full font-normal text-base
            h-24
            text-gray-700 bg-white rounded border border-solid border-gray-400
            transition ease-in outline-none
            px-3 py-1 m-0 focus:text-gray-900
            focus:border-blue-600 placeholder-gray-400 placeholder:text-xs"
                    placeholder="mock adres xyz blok türkiye -  ankara"/>
        </div>
        <div class="mb-4 flex flex-col">
          <div class="text-gray-500 text-xs mb-2">Hobilerin</div>
          <div class="flex gap-8">
            <div class="text-xs flex" v-for="item in hobbies" :key="item.id">
              <input type="checkbox" v-model="user.hobbies"
                     :value="item.id" class="h-4 w-4 mr-2 rounded border-gray-400 focus:text-blue-600">
              {{ item.name }}
            </div>
          </div>
        </div>

        <div class="mb-4 flex flex-col">
          <div class="text-gray-500 text-xs mb-2">Cinsiyet</div>
          <div class="flex gap-8">
            <div class="text-xs flex" v-for="item in genderOptions" :key="item.id">
              <input name="gender"
                     :id="item.name"
                     :value="item.id"
                     v-model="user.gender"
                     type="radio" class="h-4 w-4 mr-2 rounded border-gray-400 focus:text-blue-600">
              <label :for="item.name">{{ item.name }}</label>
            </div>

          </div>
        </div>

        <div class="mb-4 flex items-center ">
          <input @change="onFileChange" id="myFileInput" type="file" hidden ref="myFileInput">
          <button @click="$refs.myFileInput.click()"
                  :class="userValidations.file?'isError':''"
                  type="button" class="px-4 py-2  text-xs text-gray-700
         font-bold rounded outline-none border border-gray-400 leading-3 shadow-sm  w-max
         duration-150 ease-in-out  focus:shadow-lg">{{ file?.name ? 'Dosya değiştir' : 'Dosya Seç' }}
          </button>
          <span v-if="file?.name" class="ml-2 text-sm text-green-500">{{ file.name }}</span>
        </div>
        <div class="mb-4 flex items-center">
          <is-accept v-model="user.isAccept"/>
        </div>


        <button type="submit"
                class="px-4 py-2 bg-blue-600 text-white text-xs w-full
         font-bold rounded uppercase shadow-md hover:bg-blue-700 hover:shadow-lg transition
         duration-150 ease-in-out focus:bg-blue-700 focus:shadow-lg"
        >Gönder
        </button>
      </form>-->
    </div>
    <div class="p-6 rounded-md shadow-lg bg-white w-1/2 border border-solid border-gray-600">
      <p>User Info : {{ user }}</p>
      <IsAccept />
      <p>User Ülke : {{ getCountryNameById(user.country) }}</p>
    </div>
  </div>
</template>

<script>


import IsAccept from "@/components/isAccept";
import DynamicInput from "@/components/DynamicInput";

export default {
  components: {DynamicInput, IsAccept},
  methods: {
    validateData() {
      const obj = {
        name: this.user.name.trim() === "",
        surname: this.user.surname.trim() === "",
        email: this.user.email.trim() === "",
        adress: this.user.adress.trim() === "",
        file:this.user.file ? this.user.file.name?.trim()==="":true
      }
      return obj

    },
    submitMyForm() {
      const validationResult = this.validateData()
      this.userValidations = validationResult
      if (Object.values(validationResult).includes(true)) {
        alert("Form Geçersiz")
      } else {
        this.user = {
          file: '',
          gender: 3,
          name: '',
          surname: '',
          email: '',
          country: 2,
          adress: '',
          hobbies: [2],
          isAccept: true,
        }
        this.file = {}
        console.log("form gittii")
      }

    },
    onFileChange(event) {
      console.log(event.target.files)
      this.file = {name: event.target.files[0].name}
      this.user.file = {
        name: event.target.files[0].name,
        size: event.target.files[0].size,
        type: event.target.files[0].type
      }
    },
    getCountryNameById(id) {
      return this.getCountries.find((item) => item.id === id).name
    }
  },
  data() {
    return {
      genderOptions: [{id: 1, name: 'Erkek'}, {id: 2, name: 'Kadın'}, {id: 3, name: 'Belirtmek istemiyorum'}],
      hobbies: [{id: 1, name: 'Futbol'}, {id: 2, name: 'Basketbol'}, {id: 3, name: 'Satranç'}],
      countries: [{id: 1, name: 'Türkiye'}, {id: 2, name: 'Amerika'}, {id: 3, name: 'Almanya'}],
      file: {},
      userValidations: {
        name: false,
        surname: false,
        email: false,
        adress: false,
        file:false
      },
      user: {
        name: '',
        surname: '',
        email: '',
        country: 2,
        adress: '',
        hobbies: [2],
        gender: 3,
        file: '',
        isAccept: true,

      }
    }
  },
  computed: {
    getCountries() {
      return this.countries
    }
  },
  name: 'App',
}
</script>

<style>
.isError {
  @apply border-red-500;
  border-color: rgb(239 68 68 / var(--tw-border-opacity)) !important;
}

.isError:focus {
  @apply border-red-500;
}

.isError:hover {
  @apply border-red-700;

}
</style>
