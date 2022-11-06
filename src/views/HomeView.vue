<template>
  <div class="grid grid-cols-2 divide-x h-screen">
    <div class="flex justify-center bg-black items-center">
      <div class="flex-1 text-center p-4">
        <p class="text-7xl font-bold text-white">
          WaitForMe
        </p>
        <p class="text-sm text-white">A personalized waiting screen for you and your organization</p>
      </div>
    </div>
    <div class="flex justify-center bg-white items-center">
      <div class="flex-1 p-4">
        <form class="" @submit.prevent="proceeds">
          <div class="mb-4">
            <label class="block text-black font-bold mb-2 text-xl" for="username">
              Meeting's Title
            </label>
            <input
              class="shadow appearance-none border rounded w-full py-5 px-3 text-gray-700 leading-tight focus:border-solid focus:border-2" v-model="meetingTitle"
              id="username" type="text" placeholder="The meeting is about...">
          </div>
          <div class="mb-4">
            <label class="block text-black font-bold mb-2 text-xl" for="username">
              Organization's Name
            </label>
            <input
              class="shadow appearance-none border rounded w-full py-5 px-3 text-gray-700 leading-tight focus:border-solid focus:border-2" v-model="organizationName"
              id="username" type="text" placeholder="Your organization name">
          </div>
          <div class="mb-4">
            <label class="block text-black font-bold mb-2 text-xl" for="username">
              Meeting Platform
            </label>
            <select
              class="block appearance-none w-full bg-white border hover:border-gray-500 px-3 py-5 pr-8 rounded shadow leading-tight focus:border-solid focus:border-2" v-model="meetingPlatform">
              <option disabled value = "">Choose a platform</option>
              <option :value = "0">Zoom Meeting</option>
              <option :value = "1">Google Meet</option>
              <option :value = "2">Microsoft Teams</option>
            </select>
          </div>
<div class="mb-4">
            <label class="block text-black font-bold mb-2 text-xl" for="username">
              Waiting Duration
            </label>
            <select
              class="block appearance-none w-full bg-white border hover:border-gray-500 px-3 py-5 pr-8 rounded shadow leading-tight focus:border-solid focus:border-2" v-model="selected">
              <option disabled value ="">Minutes</option>
              <option class="text-gray-400" v-for="mins in avalMinutes" :key="mins" :value="mins.k">{{mins.p}}</option> 
            </select>
          </div>
          <div class="mb-4">
          <button class="bg-black w-full hover:bg-gray-800 text-white font-bold py-3 px-5 rounded">
            Show display
          </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      meetingTitle:'',
      organizationName: '',
      meetingPlatform:'',
      selected: '',
      avalMinutes: this.getAvalMins(5, 60),
    }
  },
  props:['myprop'],
  methods:{
    getCurrentTime:function(){
      const currentDate = new Date();
      let h = currentDate.getHours();
      let m = currentDate.getMinutes();
      let cTime = {hrs: h%12||12, mins: m}
      return cTime;
    },
    getAvalMins:function(mMin, mMax){
      let avMin = [];
      let minsOb = {};
      for (let index = mMin; index < mMax; index+=5) {
        minsOb = {p: `${index} Minutes`, k: index}
        avMin.push(minsOb);
      }
      console.log(avMin);
      return avMin;
    },
    proceeds:function(){
      let data = {
        "title": this.meetingTitle,
        "orgName":this.organizationName,
        "meetForm":this.meetingPlatform,
        "duration": this.selected
      };
      let all = data.title+"_"+data.orgName+"_"+data.meetForm+"_"+data.duration
      this.$router.push({
        name:'display',
        params:{
          id:all,
        }
      })

      
      
    }
  },

}
</script>

<style>

</style>
