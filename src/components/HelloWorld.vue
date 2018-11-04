<template>
  <div class="test">
    <div id="app" :style="{ 'background-color': color, 'border-color': color}">
    <div class="sample">
      <p>Input Your Color</p>
      <input type="text" min="0" max="4" v-model="color">
    </div>
  </div>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      color: '',
      num: 0,
    }
  },
  computed: {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .test {
    margin-bottom: 300px;
  }

  .sample {
    margin-top: 330px;
  }

  input {
    height: 30px;

  }

  #app {
    width: 300px;
    height: 300px;
    display: inline-block;
    margin: 0 auto;
    margin-top: 100px;
    background-color: white;
    border: 1px solid #999;
  }

</style>
