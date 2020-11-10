<template>
  <div class="flex items-center justify-between p-3 bg-gray-100">
    <div class="w-8/12">
      <textarea v-model="text" @change="onTextChange" rows="10" class="w-full p-2 border border-solid border-gray-300 focus:border-gray-500"></textarea>
    </div>
    <div class="w-4/12 flex justify-center">
      <img v-if="url" :src="url" alt="QrCode">
    </div>
  </div>
</template>

<script>
import qrcode from 'qrcode'
export default {
  name: "QrCode",
  data(){
    return {
      text: 'The text',
      url: '',
      options: {
        errorCorrectionLevel: 'M',
        width: 300,
      }
    }
  },
  methods:{
    createQrCode(){
      if (this.text){
        qrcode.toDataURL(this.text, this.options).then(url=>{
          this.url = url
        })
      }
    },

    onTextChange(){
      this.createQrCode()
    },
  },
  mounted() {
    this.createQrCode()
  },
}
</script>

<style scoped>

</style>