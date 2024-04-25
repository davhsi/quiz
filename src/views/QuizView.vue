<script setup>
    import Question from '@/components/Question.vue';
    import QuizHeader from '@/components/QuizHeader.vue';
    import { ref, watch, computed } from 'vue';
    import {useRoute } from "vue-router"
    import q from "../data/quizes.json"
import Result from '@/components/Result.vue';

    const route = useRoute()
    const quizId = parseInt(route.params.id)
    const quiz = q.find(q => q.id === quizId )
    const currentQuestionIndex = ref(0)
    const numberOfCorrectAnswers = ref(0)
    const showResults = ref(false)


    // const questionStatus = ref(`${currentQuestionIndex.value}/${quiz.questions.length}`)
    // watch(()=>currentQuestionIndex.value, () => {
    //     questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`
    //     console.log(questionStatus)
    // })
    
    /* computed is used to update a state if there is a change in another state */
    const questionStatus = computed(() => `${currentQuestionIndex.value}/${quiz.questions.length}`)
    const barPercentage = computed(() => `${currentQuestionIndex.value/quiz.questions.length * 100}%`)
    
    const onOptionSelected = (isCorrect) => {
        if(isCorrect){
            numberOfCorrectAnswers.value++
        }
        if(quiz.questions.length -1 === currentQuestionIndex.value){
            showResults.value=true
        }
        currentQuestionIndex.value++
    }
</script>

<template>
    <QuizHeader
        :questionStatus= "questionStatus"
        :barPercentage = "barPercentage"
    />

    <div>
        <Question
            v-if="!showResults"
            :question="quiz.questions[currentQuestionIndex]"
            @selectOption="onOptionSelected"
        />
        <Result
            v-else
            :quizQuestionLength ="quiz.questions.length"
            :numberOfCorrectAnswers ="numberOfCorrectAnswers"
        />
    </div>
</template>