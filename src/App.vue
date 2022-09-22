<script>
  export default{
    data(){
      return{
      add:{
        desc:"",
        incomeValue: null,
        date:"",
        // id:null
      },
        toTalIncome:0,
        allData : []
      }
    },
    methods:{
      submit(){

        // this.add.id = Date.now()
        if(typeof(this.add.incomeValue) == "number" ) this.toTalIncome += parseInt(this.add.incomeValue)
       this.allData = [...this.allData,{...this.add, id:Date.now()}]
       this.allData.sort((a,b) => Date.parse(b.date) - Date.parse(a.date))
        this.add.desc = "",
        this.add.incomeValue = null
        this.add.date = ""

      },
      remove(id){
        this.allData = this.allData.filter(data => data.id != id)
      }
    }
  }
</script>

<template >
  <div>
    <div class="bg-gray-700   text-center border-b-8 border-blue-500 ">
      <div class="w-10/12 px-20 py-10 mx-auto text-white flex justify-between   ">
        <h2> Income Tracker</h2>
        <h2 class="min-w-[80px] px-7 py-1  rounded-lg  bg-blue-500 ">{{toTalIncome}}</h2>
      </div>
    </div>


    <div class="w-10/12 mx-auto  flex justify-center py-10 drop-shadow-2xl ">
      <input v-model="add.desc" class="myInput rounded-l-lg" placeholder="Income Description" type="text">
      <input v-model="add.incomeValue" class="myInput " placeholder="Income Value" type="number">
      <input v-model="add.date" class="myInput  text-center" type="date">
      <button @click="submit" class="btnBlue rounded-l-none text-xl px-6">Submit</button>
    </div>

    <div  class="w-8/12 mx-auto py-10   text-xl text-slate-600  font-semibold ">
      <div v-for="data in allData" :key="data.id"  class="flex justify-center  rounded-lg bg-white  my-8">

        <span class=" w-1/12 flex justify-center items-center text-red-400  ">
          <svg @click="remove(data.id)" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" 
          class="w-8 h-8 hover:border-2 "><path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" /></svg>
        </span>
        <span class="w-5/12   p-3">{{data.desc}}</span>
        <span class="w-3/12 ml-7 p-3">{{data.incomeValue}}</span>
        <span class="w-3/12 ml-7 p-3">{{data.date}}</span>

      </div>

    </div>

  </div>
</template>

<style>

</style>
