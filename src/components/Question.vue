<script setup>
    import {defineEmits} from "vue"
    const {question} = defineProps(['question'])
    const emit = defineEmits(["selectOption"])

    const emitSelectedOption = (isCorrect) => {
        emit("selectOption",isCorrect)
    }   
</script>

<template>
    <div class="question-container">
            <p class="question">
                {{ question.text }}
            </p>
        </div>

        <div 
            v-for="option in question.options" 
            key="option.id" 
            class="option-container"
            @click="emitSelectedOption(option.isCorrect)"
        >
            <div class="option">
                <p class="option-label">{{option.label}}</p>
                <div class="option-value">{{option.text}}</div>
            </div>
            
            
        </div>
</template>


<style scoped>
    .question-container{
        margin-top: 20px;
    }
    .question{
        margin-bottom: 20px;
        font-size: 30px;
    }

    .option{
        display:flex;
        margin-bottom: 20px;
        cursor: pointer;
    }

    .option-label{
        background-color: bisque;
        height:50px;
        width:50px;
        font-size: 30px;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .option-value{
        background-color: rgb(244,239,239);
        width:100%;
        font-size: 30px;
        padding: 0 20px;
    }
</style>