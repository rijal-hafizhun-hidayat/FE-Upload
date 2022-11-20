<template>
  <div class="about">
    <input type="text" v-model="data.ini">
    <!-- <input type="file" @input="data.gambar = $event.target.files[0]"> -->
    <button @click="upload">submit</button>
  </div>
</template>

<script>
import { reactive, ref } from '@vue/reactivity'
import axios from 'axios';

export default {
  setup(){
    const data = reactive({
      ini: ''
    });
    
    function upload(){
      const config = {
        headers: {
          'Content-Type': "multipart/form-data; charset=utf-8; boundary=" + Math.random().toString().substr(2)
        }
      }
      let x = new FormData();
      x.append('ini', data.ini)
      axios.post(`http://127.0.0.1:8000/api/image`, x, config)
      .then((res) => {
        console.log(res)
      }).catch((err) => {
        console.log(err)
      })
    }

    return{
      data, upload
    }
  }
}
</script>
<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
