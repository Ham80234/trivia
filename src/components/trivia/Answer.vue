<template >
    <div>
        <button :disabled="reveal" :class="reveal ? (answer.correct ? 'correct' : 'incorrect'): ''" @click="$emit('testCase', 'reveal'), handleClick()">
            {{ answer.question }}
        </button>
    </div>
</template>
<script>
export default {
    name: "Answer",
    props: {
        answer: Object,
        reveal: Boolean
    },
    methods: {
        handleClick() { 
            if (this.answer.correct){
                this.$emit('correctAnswer')
            }
        }
    }
}
</script>
<style lang="css" scoped>
     button {
        background: transparent;
        color: #ffbd00;
        border: 1px solid #ffbd00;
        min-height: 50px;
        min-width: 350px;
        border-radius: 15px;
        margin: auto;
    }
    .correct {
        color: #049907;
        border: 1px solid #049907;
    }
    .incorrect { 
        color: #990e04;
        border: 1px solid #990e04;
    }
</style>pro