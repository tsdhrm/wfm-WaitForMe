<template>
  <div class="flex flex-col bg-white p-20 h-screen">
    <div class="flex flex-row h-screen mb-3 space-x-40">
      <div class="flex flex-col p-5 w-4/6 leading-relaxed">
        <div class="flex flex-col h-5/6">
          <h1 class="text-5xl font-bold">Hello there,</h1>
          <h1 class="text-5xl font-bold mb-2">thanks for joining our online meeting!</h1>
          <p class="text-md font-medium text-gray-500 mb-3">
            Online meetings can be overwhelming by some people, so we'll start the meeting effectively at {{timeEnds}}. While you wait,
            please enjoy some news article and review the meeting information (or grab yourself some snacks enjoy some drinks!).
          </p>
            <!--
          <p class="text-3xl font-medium text-gray-700 mb-10" v-if="!expired">
            {{displayHours}}:{{displayMinutes}}:{{displaySeconds}} until start.
          </p>
          <p class="text-3xl font-medium text-gray-700 mb-10" v-else>
            The meeting begin.
          </p> -->
        </div>
        <div class="flex flex-col h-1/6">
          <p class="text-sm mb-1 uppercase tracking-widest font-bold"> 
            Meeting's Information
          </p>
          <p class="text-sm tracking-normal text-gray-500">
            "{{allData[0]}}" by {{allData[1]}}
          </p>
          <p class="text-sm tracking-normal text-gray-500">
            Helded through {{platform}}
          </p>
        </div>
      </div>
      <div class="flex w-100 w-2/6 justify-center p-5">
        <NewsCardComp/>
      </div>
    </div>
    <div class="flex text-white justify-center">
      <div class="text-gray-300 text-sm "> Press "q" to exit display mode </div>
    </div>
  </div>
</template>

 <script>
  import NewsCardComp from '../components/NewsCardComp.vue' 
  export default {
    components:{
      NewsCardComp,
    },
    data(){
      return{
        allData: [],
        platform: "",
        timeEnds: "",
        displayDays: 0,
        displayHours: 0,
        displayMinutes: 0,
        displaySeconds: 0,
        expired: false,
      }
      
    },
    mounted() {
      this.splitData();
      this.setEndTime();
      this.showRemaining();
    },
    methods: {
      splitData:function(){
        let datas = this.$route.params.id;
        this.allData = datas.split("_");
        if (this.allData[2] == 0){
          this.platform = "Zoom Meeting";
        }else if (this.allData[2] == 1){
          this.platform = "Google Meet";
        }else{
          this.platform = "Microsoft Teams";
        }
      },
      setEndTime:function(){
        const d = new Date()
        let hrs = d.getHours();
        let mins = d.getMinutes();
        this.timeEnds = hrs+":"+(parseInt(mins)+parseInt(this.allData[3]));
      },
      showRemaining(){
        const timer = setInterval(() => {
          const now = new Date();
          const nowYear = parseInt(now.getFullYear());
          const nowMonth = parseInt(now.getMonth());
          const nowDate = parseInt(now.getDate());
          const nowHours = parseInt(now.getHours());
          const nowMinutes = parseInt(now.getMinutes());
          let newMinutes = parseInt(this.allData[3])
          newMinutes = nowMinutes+newMinutes;
          console.log(newMinutes);
          const end = new Date(nowYear, nowMonth, nowDate, nowHours, newMinutes,0, 10);
          const distance = end.getTime() - now.getTime();
          if (distance < 0){
            clearInterval(timer);
            this.expired = true;
            return
          }
          const days = Math.floor((distance/this._days));
          const hours = Math.floor((distance % this._days)/this._hours);
          const minutes = Math.floor((distance % this._hours)/this._minutes);
          const seconds = Math.floor((distance % this._minutes)/this._seconds);

          this.displayMinutes = minutes < 10 ? "0" + minutes : minutes;
          this.displaySeconds = seconds < 10 ? "0" + seconds : seconds;
          this.displayHours = hours < 10 ? "0" + hours : hours;
          this.displayDays = days < 10 ? "0" + days : days;
        }, 1000);
      }
    },
    computed: {
      _seconds:()=> 1000,
      _minutes(){
        return this._seconds*60;
      },
      _hours(){
        return this._minutes*60;
      },
      _days(){
        return this._hours*24;
      }
      
    },
  }
 </script>

<style>
  
</style>
   
