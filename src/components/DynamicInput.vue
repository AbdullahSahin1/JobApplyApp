<template>
  <div class="flex flex-col">
    <div class="flex gap-8" v-for="item in userExp" :key="item.company">
      <div class="mb-4 flex flex-col w-full">
        <label for="nameInput" class="text-gray-500 text-xs mb-2">Şirket Adı</label>
        <input id="nameInput"
               v-model="item.company"
               class="block w-full font-normal text-base
            text-gray-700 bg-white rounded border border-solid border-gray-400
            transition ease-in outline-none
            px-3 py-1 m-0 focus:text-gray-900
            focus:border-blue-600 placeholder-gray-400 placeholder:text-xs"
               placeholder="John"
        >
      </div>
      <div class="mb-4 flex flex-col w-full">
        <label for="expInput" class="text-gray-500 text-xs mb-2">Deneyim Yılı</label>
        <input id="expInput"
               v-model="item.exp"
               class="block w-full font-normal text-base
            text-gray-700 bg-white rounded border border-solid border-gray-400
            transition ease-in outline-none
            px-3 py-1 m-0 focus:text-gray-900
            focus:border-blue-600 placeholder-gray-400 placeholder:text-xs"
               placeholder="3+"
        >
      </div>
    </div>
  </div>
    <h1 >Toplam Deneyim Yılı : {{getTotalYears}} </h1>
  <button
      type="button" @click="addNewExp()" class="px-4 py-2  text-xs text-gray-700
         font-bold rounded outline-none border border-gray-400 leading-3 shadow-sm  w-max
         duration-150 ease-in-out  focus:shadow-lg">Tecrübe Ekle +
  </button>
</template>

<script>
export default {
  name: "DynamicInput",
  methods:{
    addNewExp(){
      this.userExp.push({
        company: '',
        exp:''
      })
    }
  },
  computed:{
      getTotalYears(){
        let totalYear=0
        this.userExp.forEach((item)=>{
          totalYear+=Number(item.exp)
        })
        return totalYear;
      }
  },
  data(){
    return{
      userExp:[{
        company:'',
        exp:''
      }]
    }
  }
}
</script>

<style scoped>

</style>
