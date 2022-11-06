<template>
  <div class="flex flex-col bg-white p-20 h-screen">
    <div class="flex flex-row h-screen mb-3 space-x-40">
      <div class="flex flex-col p-5 w-4/6 leading-relaxed">
        <div class="flex flex-col h-5/6">
          <h1 class="text-5xl font-bold">Hello there,</h1>
          <h1 class="text-5xl font-bold mb-2">thanks for joining our online meeting!</h1>
          <p class="text-md font-medium text-gray-500 mb-3">
            Online meetings can be overwhelming by some people, so we'll start the meeting effectively at 7:10 PM. While you wait,
            please enjoy some news article and review the meeting information (or grab yourself some snacks enjoy some drinks!).
          </p>
          <p class="text-3xl font-medium text-gray-700 mb-10">
            00:09:30 until start.
          </p>
        </div>
        <div class="flex flex-col h-1/6">
          <p class="text-sm mb-1 uppercase tracking-widest font-bold"> 
            Meeting's Information
          </p>
          <p class="text-sm tracking-normal text-gray-500">
            "December's Prep" by KMHD Pascasarjana UGM
          </p>
          <p class="text-sm tracking-normal text-gray-500">
            Helded through Zoom Meeting
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
    }
    
  }
 </script>

<style>
  
</style>
   
