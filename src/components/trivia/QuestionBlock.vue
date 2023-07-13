<template >
    <div class="container" v-if="questionText">
       <h1>{{ this.questionText }}</h1>
        <div v-for="i in questionOptions">
            <Answer :answer="i" @test-case="revealAnswer" @correct-answer="correct += 1" :reveal="reveal" />
        </div>
        <button class="next" @click="this.getQuestion" v-if="showNext">Next Question</button>
        <h4>{{ correct }}/{{ count }}</h4>
    </div>
</template>
<script>
import axios from 'axios';
import Answer from './Answer.vue';

export default {
    name: "QuestionBlock",
    components: {
        Answer
    },
    data () { 
        return { 
            questionText: null,
            questionOptions: [],
            reveal: false,
            showNext: true,
            count: 0,
            correct: 0
        }
    },
    created: function () { 
            this.getQuestion()
    },
    methods: {
        revealAnswer: function (q) {
            console.log();
            this.reveal = true
            this.showNext = true
            this.count++
        },
        getQuestion: function () { 
            this.showNext = false
            this.reveal = false
            this.questionOptions = []
            axios.get('https://the-trivia-api.com/v2/questions?limit=1')
            .then((res) => {
                this.questionText = res.data[0].question.text
                res.data[0].incorrectAnswers.forEach(element => {
                    let item = {
                        question: element,
                        correct: false,
                        reveal: false
                    }
                    this.questionOptions.push(item)
                });
                this.questionOptions.push({question: res.data[0].correctAnswer, correct: true, reveal: false})
                console.log(this.questionOptions)
                this.questionOptions.sort(() => (Math.random() > .5) ? 1 : -1)
            })
        }
    }
}
</script>
<style lang="css" scoped> 
    .container{ 
        color: #ffbd00;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        padding: 25px;
        text-align: center;
        gap: 10px;
        max-width: 400px;
        margin: auto;
    }
    h1 {
        padding-bottom: 40px;
    }
    button {
        background: transparent;
        color: #ffbd00;
        border: 1px solid #ffbd00;
        min-height: 50px;
        min-width: 350px;
        border-radius: 15px;
    }
    .next{
        color: #ec814c;
        border-color: #ec814c;
    }
</style>