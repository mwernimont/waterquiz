<template>
  <div id="visualization">
    <Quiz />
  </div>
</template>

<script>
    import Quiz from "../components/Quiz"
    export default {
        name: 'Visualization',
        components:{
          Quiz
        }
    }
</script>

<style scoped lang="scss">
#visualization{
  background: red;
  /* #app is the flex parent set in App.vue */
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 10px;
}
</style>
