<template>
    <div id="results">
        <div id="resultText">
            <h1>Congrats on Finishing the Quiz!</h1>
            <p>Here are your results:</p>
        </div>
        <div id="resultScores">
            <div class="result">
                <h3>Correct</h3>
                <div id="correctResult" class="resultCount"></div> 
            </div>
            <div class="result">
                <h3>Incorrect</h3>
                <div id="incorrectResult" class="resultCount"></div> 
            </div>
        </div>
        <div class="drippyExcited">
            <excitedDrippy  />
        </div>
        <div id="buttons">
            <a class="button resultButton" href="https://www.usgs.gov/special-topic/water-science-school">
                Learn More
            </a>
            <button @click="retryQuiz" class="button resultButton">Retry Quiz</button>
        </div>
    </div>
</template>
<script>
import excitedDrippy from "@/assets/images/drippy/drippyExcited.svg";
export default {
    name: "Results",
    components: {
        excitedDrippy 
    },
    mounted(){
        let correct = document.getElementById("correctResult");
        let incorrect = document.getElementById("incorrectResult");

        correct.innerHTML = this.$parent.correctScore;
        incorrect.innerHTML = this.$parent.incorrectScore;
    },
    methods:{
        retryQuiz(){
            this.$parent.RetryQuiz();
        }
    }
}
</script>
<style lang="scss" scoped>
#results{
    text-align: center;
}
#resultText{
    h1{
        font-size: 20pt;
        margin: 0 0 10px 0;
    }
    p{
       font-size: 16pt; 
       margin: 0 0 0 0;
    }
}
#resultScores{
    display: flex;
    margin: 20px 0;

}
.result{
    flex: 1;
    h3{
        font-size: 24pt;
    }
    .resultCount{
        font-size: 38pt;
    }
}
#buttons{
    display: flex;
    align-items: center;
    justify-content: center;
    a{
        text-decoration:none;
    }
}
.resultButton{
    flex: 1;
    font-size: 1.5em;
    max-width: 195px;
    &:first-child{
        margin-right: 10px;
    }
}
@media screen and (min-width: 600px){
    #resultText{
        h1{
            font-size: 38pt;
        }
        p{
            font-size: 24pt;
        }
    }
}
</style>