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
        <form class="">
          <div class="mb-4">
            <label class="block text-black font-bold mb-2 text-xl" for="username">
              Meeting's Title
            </label>
            <input
              class="shadow appearance-none border rounded w-full py-5 px-3 text-gray-700 leading-tight focus:border-solid focus:border-2"
              id="username" type="text" placeholder="The meeting is about...">
          </div>
          <div class="mb-4">
            <label class="block text-black font-bold mb-2 text-xl" for="username">
              Organization's Name
            </label>
            <input
              class="shadow appearance-none border rounded w-full py-5 px-3 text-gray-700 leading-tight focus:border-solid focus:border-2"
              id="username" type="text" placeholder="Your organization name">
          </div>
          <div class="mb-4">
            <label class="block text-black font-bold mb-2 text-xl" for="username">
              Meeting Platform
            </label>
            <select
              class="text-gray-400 block appearance-none w-full bg-white border hover:border-gray-500 px-3 py-5 pr-8 rounded shadow leading-tight focus:border-solid focus:border-2">
              <option>Choose your meeting platform</option>
              <option>Zoom Meeting</option>
              <option>Google Meet</option>
              <option>Microsoft Teams</option>
            </select>
          </div>
          <div class="mb-4">
            <label class="block text-black font-bold mb-2 text-xl" for="username">
              Wait until
            </label>
            <div class="shadow appearance-none border rounded w-full py-5 px-3 text-gray-700 leading-tight focus:border-solid focus:border-2 inline-flex text-xl justify-center">
              <select name="" id="" class="px-2 outline-none appearance-none bg-transparent">
                <option class="focus:border-solid focus:border-2" v-for="n in rangeF(currentTime.hrs,12)" :key="n" :value="n">{{n}}</option>
              </select>
              <span class="px-2">:</span>
              <select name="" id="" class="px-2 outline-none appearance-none bg-transparent">
                <option v-for="n in rangeF(currentTime.mins,59)" :key="n" :value="n">{{n}}</option>
              </select>
              <select name="" id="" class="px-2 outline-none appearance-none bg-transparent">
                <option value="AM">AM</option>
                <option value="PM">PM</option>
              </select>
            </div>
          </div>
          <div class="mb-4">
            <button class="bg-black w-full hover:bg-gray-800 text-white font-bold py-3 px-5 rounded">
              Display waiting screen
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
      currentTime: this.getCurrentTime(),
      meetingTitle:'',
      organizationName: '',
      meetingPlatform:'',
      waitUntil:{
        hrs: '',
        mins: '',
        amPM: '',
      },
      avalHrs : this.rangeF(1, 12),
    }
  },
  methods:{
    getCurrentTime:function(){
      const currentDate = new Date();
      let h = currentDate.getHours();
      let m = currentDate.getMinutes();
      let cTime = {hrs: h%12||12, mins: m}
      return cTime;
    },
    rangeF:function(min, max){
      let newMin = 0;
      if (min == 12){
        newMin = 0;
      }else{
        newMin=min
      }
      let array = [], j =0;
      for (let i = newMin; i<=max; i++){
        array[j] = i;
        j++;
      }
      return array;
    }
  }

}
</script>

<style>

</style>