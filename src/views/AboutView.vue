<template lang="">
  <div>
    <h1>{{ this.params[0] }}</h1>
    <h3>{{ this.params[1] }}</h3>
    <!-- <img :src="this.params" alt=""> -->
    <button @click="paramsCheck"></button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      params: this.$route.params.id.split("+"),
    };
  },
  updated() {
    console.log(this.$route.params.id);
  },
  methods:{
    paramsCheck: function (){
      console.log(this.$route.params)
    }
  }
};
</script>
<style lang=""></style>
