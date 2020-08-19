<template>
    <div id="container">
        <div id="quizContainer">
            <div id="questionCount"></div>
            <div id="questionOutcome" v-show="outcome">
                <div class="usa-accordion usa-accordion--bordered">
                    <h2 class="usa-accordion__heading">
                        <button class="usa-accordion__button"
                            aria-expanded="false"
                            aria-controls="a1">
                            Remind Me of the Question
                        </button>
                    </h2>
                    <div id="a1" class="usa-accordion__content usa-prose">
                        <p id="previousQuestion"></p>
                    </div>
                </div>
                <div id="answerResult"></div>
                <div id="explanation"></div>
                <div id="illustration">
                    <DynamicIcon :icon="icon" />
                </div>
                <button @click="NextQuestion();" id="nextQuestion" class="button">Next Question</button>
            </div>
            <div id="quiz" v-show="quizzing">
                <div id="question"></div>
                <div id="scores">
                    <div class="score">
                        <h3>Correct</h3>
                        <div id="correct">
                            <div id="correctCount" class="scoreCount">0</div> 
                        </div>
                    </div>
                    <div class="score">
                        <h3>Incorrect</h3>
                        <div id="incorrect">
                            <div id="incorrectCount" class="scoreCount">0</div> 
                        </div>
                    </div>
                </div>
                <div id="answers">
                    <div id="true" class="answer">
                        <button @click="CheckAnswer($event)" class="option button">TRUE</button>
                    </div>
                    <div id="drippy">
                        <drippyAsksQuestion />
                    </div>
                    <div id="false" class="answer">
                        <button @click="CheckAnswer($event)" class="option button">FALSE</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import quizData from "@/assets/quiz/quiz.json";
import drippyAsksQuestion from "@/assets/images/drippy/drippyAsksQuestion.svg";
import DynamicIcon from "./DynamicIcon";
export default {
    "name": "Quiz",
    components:{
        DynamicIcon,
        drippyAsksQuestion
    },
    data(){
        return{
            quizzing: true,
            outcome: false,
            correctScore: 0,
            incorrectScore: 0,
            index: 0,
            questions: [],
            answers: [],
            explanations: [],
            icon: "question1"
        }
    },
    mounted(){
        this.BuildQuiz();
        // This is a fix for the weird USWDS glitch that causes the Methods section accordion menus to be open on page load
        const targetAccordionDivs = document.querySelectorAll('div.usa-accordion__content');
        targetAccordionDivs.forEach((div) => {
            div.setAttribute('hidden', '""');
        });
    },
    methods:{
        BuildQuiz(){
            let self = this;
            quizData.forEach(function(current){
                self.questions.push(current.Question);
                self.answers.push(current.Answer);
                self.explanations.push(current.Explanation);
            });
            this.AskQuestion();
        },
        AskQuestion(){
            let questionCount = document.getElementById("questionCount");
            let question = document.getElementById("question");
            let correctCount = document.getElementById("correctCount");
            let incorrectCount = document.getElementById("incorrectCount");

            correctCount.innerHTML = this.correctScore;
            incorrectCount.innerHTML = this.incorrectScore;

            questionCount.innerHTML = "Question " + (this.index + 1) + " of " + this.questions.length;
            question.innerHTML = this.questions[this.index];
        },
        CheckAnswer(event){
            let answer = JSON.parse(event.target.innerHTML.toLowerCase());
            this.outcome = true;
            
            if(this.answers[this.index] === answer){
                this.correctScore++;
                this.ShowRoundResult("Correct")
            }else{
                this.incorrectScore++;
                this.ShowRoundResult("Incorrect")
            }
        },
        ShowRoundResult(result){
            this.quizzing = false;
            let previousQuestion = document.getElementById("previousQuestion");
            let answerResult = document.getElementById("answerResult");
            let explanation = document.getElementById("explanation");
            let illustration = document.getElementById("illustration");

            previousQuestion.innerHTML = this.questions[this.index];
            explanation.innerHTML = this.explanations[this.index];
            answerResult.innerHTML = result;

            this.index++;
        },
        NextQuestion(){
            this.icon = "question" + (this.index + 1);
            console.log(this.icon);
            if(this.index <= 14){
                this.outcome = false;
                this.quizzing = true;
                this.AskQuestion();
            }else{
                console.log("Quiz Finished");
            }
        }
    }
}
</script>
<style lang="scss" scoped>
@import url("https://use.typekit.net/ahv6btz.css");
$chevronLeft: '~@/assets/images/chevrons/chevron-left.png';
$chevronDown: '~@/assets/images/chevrons/chevron-down.png';
    #container{
        width: 100%;
        max-width: 800px;
    }
    #quizContainer{
        flex: 1;
        padding: 10px;
        
        font-size: 14pt;
    }
    .button{
        padding: 10px;
        border-radius: 5px;
        border: none;
        background: rgb(0,168,212);
        outline: none;
        color: #fff;
        font-weight: 700;
    }
    #questionCount{
        font-weight: 700;
        margin-bottom: 10px;
    }
    #question{
        width: 100%;
        margin: 0 0 20px 0;
    }
    #scores{
        min-height: 30px;
        display: flex;
        margin-bottom: 20px;
    }
    .score{
        min-height: 30px;
        flex: 1;
        text-align: center;
        h3{
            margin: 0 0 10px 0;
            font-size: 1em;
        }
        .scoreCount{
            font-size: 2em;
        }
    }
    #answers{
        min-height: 40px;
        display: flex;
    }
    .answer{
        flex: 1;
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
        button{
            width: 100%;
        }
    }
    #drippy{
        flex: 2;
    }
    .usa-accordion{
        font-family: din-2014, sans-serif;
        .usa-accordion__heading{
            
            .usa-accordion__button{
                font-size: 1em;
                font-weight: 400;
                padding: 10px;
                outline: none;
            }
        }
        .usa-accordion__content{
            padding: 10px;
        }
        .usa-prose > p{
            max-width: 100ex;
        }
        .usa-accordion__button{
            background-image: url($chevronDown);
            background-size: 15px 10px;
            border-radius: 5px 5px 0 0;
        }
        .usa-accordion__button[aria-expanded=false]{
            background-image: url($chevronLeft);
            background-size: 10px 15px;
            border-radius: 5px;
        }
    }
    #questionOutcome{
         text-align: center;
    }
    #answerResult{
        margin: 20px 0;
        font-size: 30pt;
        font-weight: 700;
    }
    #illustration{
        width: 150px;
        height: 150px;
        margin: 20px auto;
    }

</style>