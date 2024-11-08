<template>
  <div>
    <h1>{{message}}</h1>
    <button @click="changeMessage">Change Message</button>
  </div>
</template>
<script>
export default {
  data(){
    return{
      message: "Hello from Yamakasi"
    };
  },
  methods: {
    changeMessage(){
      this.message = "Message changed with sfc!!!"
    }
  }
};
</script>
<style scoped>
 h1{
   color: lawngreen;
 }
</style>