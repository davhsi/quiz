<script setup>
  import q from '../data/quizes.json';
  import { ref, watch } from "vue";
  import Card from "../components/Card.vue"

  const quizes = ref(q);

  const search = ref("");
  watch(search, () => {
    quizes.value = q.filter(quiz => quiz.name.toLowerCase().includes(search.value.toLowerCase()))
  })

</script>
<template>
  <div>
    <header>
      <h1>Quiz</h1>
      <input  v-model.trim="search" type="text" placeholder="Search...">
    </header>

    <div class="card-container">
      <Card v-for="quiz in quizes" :key="quiz.id" :quiz="quiz"/>
      <!-- <div v-for="quiz in quizes" :key="quiz.id" class="card">
        <img :src="quiz.img">
        <div class="card-text">
          <h2>{{ quiz.name }}</h2>
          <p>{{ quiz.questions.length }} questions</p>
        </div>
      </div> -->
    </div>
    
  </div>
</template>

<style scoped>

  header{
    margin-top: 30px;
    margin-bottom: 10px;
    align-items: center;
    justify-content: space-between;
    display: flex;
    align-items: center;
  }

  header h1{
    font-weight: bold;
    margin-right: 30px;
  }

  header input{
    border: none;
    border-radius: 5px;
    padding: 10px;
    background-color: rgba(234, 234, 242, 0.518)

  }

  /* CARD */
  .card-container{
    display: flex;
    flex-wrap: wrap;
    margin-top: 40px;
  }

  .card {
    width: 310px;
    overflow: hidden;
    border-radius: 2%;
    box-shadow: 1px 1px 10px rgba(0,0,0,0.1);
    margin-bottom: 35px;
    margin-right: 20px;
    cursor: pointer;
  }

</style>