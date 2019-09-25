<template>
  <div class="home">
    <div class="wrap">
      <div class="content">
        <h1>The Weather</h1>
        <hr>
        <h2 style="padding-top: 20px">How to use ?</h2>
        <p style="white-space: pre-line; line-height: 1.8; padding-top: 20px;">You should refer to the weather page and choose your city (Ukraine).
           If you do not choose a city, the app will take your geolacation. It is all. Have fun from using ! ;)</p>
      </div>
      <span class="made-by">Made by <a href="https://github.com/dmoneone">dmoneone</a></span>
    </div>
  </div>
</template>
<style scoped>
  .home{
    padding: 30px;
    height: 90vh;
  }
  .wrap{
    display: flex;
  	flex-direction: column;
  	min-height: 100%;
  }
  .content{
    flex: 1 0 auto;
  }
  .made-by{
    flex: 0 0 auto;
  }
</style>
<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
  }

}
</script>
