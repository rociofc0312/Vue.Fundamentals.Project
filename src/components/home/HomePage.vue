<template>
  <div class="home">
    <div>
      <img src="../../assets/home-images/robot-home.png" alt="" class="robot">
    </div>
    <div>
      <router-link to="/build">Get started</router-link> building your fist robot!
    </div>
  </div>
</template>

<script>
export default {
  name: 'HomePage',
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.home {
  text-align: center;
}
.robot{
  height: 300px;
}
</style>
