<template>
    <div id="quizContainer">
        <div id="questionCount"></div>
    </div>
</template>
<script>
export default {
    "name": "Quiz"
}
</script>
<style lang="scss" scoped>
    #quizContainer{
        background: purple;
        flex: 1;
        padding: 10px;
        max-width: 800px;
    }
    #questionCount{
        background: lime;
        width: 100px;
        min-height: 30px;
    }
</style>