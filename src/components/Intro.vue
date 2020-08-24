<template>
    <div id="Intro">
        <div id="quizTitle">
            <h1>Water Properties Quiz</h1>
            <p>Hosted by Drippy</p>
        </div>
        <div id="drippyExcited">
            <excitedDrippy />
        </div>
        <div id="begin">
            <button @click="beginQuiz" class="button">Begin Quiz</button>
        </div>
    </div>
</template>
<script>
import excitedDrippy from "@/assets/images/drippy/drippyExcited.svg";
export default {
    name: "Intro",
    components:{
       excitedDrippy 
    },
    methods: {
        beginQuiz(){
            this.$parent.BeginQuiz();
        }
    }
}
</script>
<style lang="scss" scoped>
$drippyBlue: rgb(60, 199, 244);
#Intro{
   text-align: center;
}
#quizTitle{
    h1{
        margin: 0 0 10px 0;
        font-size: 28pt;
        color: $drippyBlue;
    }
    p{
        font-size: 16pt;
        margin: 0 0 20px 0;
    }
}
#drippyExcited{
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 20px;

    svg{
        max-width: 400px;
        flex: 1;
    }
}
#begin{
    font-size: 1.5em;
}
@media screen and (min-width: 600px){
    #quizTitle{
        h1{
            font-size: 38pt;
        }
        p{
            font-size: 24pt;
        }
    }
}
</style>