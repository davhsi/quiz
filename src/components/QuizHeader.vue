<script setup>
    const {
        questionStatus,
        barPercentage
    } = defineProps([
        "questionStatus",
        "barPercentage"
    ])
</script>

<template>
    <header>
        <h4>Question {{ questionStatus }}</h4>
        <div class="bar">
            <div class="completion-status" :style="{width:barPercentage}">
            </div>
        </div>
    </header>
</template>

<style scoped>
    header{
        margin-top: 20px;
    }
    header h4{
        font-size: 40px;
    }

    .bar{
        border: 3px solid bisque;
        width: 300px;
        height:50px
        
    }

    .completion-status{
        height: 100%;
        background-color: bisque;
        width: 10%;

    }
</style>