<script setup>
import q from "../data/quizz.json"
import { ref,watch } from "vue";
import Card from "../components/Card.vue"

const quizzs = ref(q)

const search = ref("")

watch(search,()=>{
  console.log("hello from watch")
  quizzs.value = q.filter(quiz=>quiz.name.toLowerCase().includes(search.value.toLocaleLowerCase()))
})

</script>


<template>
  <div>
    
    <header>
      <h1>quizzes</h1>
      <input v-model.trim="search" @keypress="performSearch" type="text" placeholder="Search" />
    </header>
    <div class="options-container"  >
      <Card v-for="quiz in quizzs" :key="quiz.id" :quiz="quiz" />
    </div>
  </div>
</template>
<style scoped>

header{
  margin-bottom: 10px;
  margin-top: 30px;
  display: flex;
  align-items: center;
}
  header h1{
    font-weight: bold;
    margin-right: 30px;
  }
  header input{
    border:none;
    background-color: rgba(128, 128, 128, 0.1);
    padding: 10px;
    border-radius: 5px;

  }
.options-container{
  display: flex;
  flex-wrap: wrap;
  margin-top: 30px;
}
 

</style>
