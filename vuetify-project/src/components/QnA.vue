<script setup>
import { ref, computed } from 'vue';

const currentPage = ref(1);
const itemsPerPage = 5;
const questions = ref([]); 

const paginatedQuestions = computed(() => {
  const startIndex = (currentPage.value - 1) * itemsPerPage;
  const endIndex = startIndex + itemsPerPage;
  return questions.value.slice(startIndex, endIndex);
});

function changePage(page) {
  currentPage.value = page;
}

function removeQuestion(question) {
  questions.value = questions.value.filter(q => q.id !== question.id);
}

const questionData = ref([]);

async function getList() {
    const res = await fetch(`http://localhost:3001/Question`);
    questionData.value = await res.json(); 
}
getList(); 

function submitForm(event) {
    event.preventDefault(); 
    const form = new FormData(event.target); 
    const newQuestion = form.get('question'); 
    addQuestion(newQuestion); 
}

function addQuestion(newQuestion) {
    if (newQuestion.trim() !== '') {
        questionData.value.push({
            title: newQuestion,
            content: '' // 내용은 비워둠
        });
    }
}
</script>

<template>
<<<<<<< HEAD
<<<<<<< HEAD
=======
>>>>>>> 6d62b3918dd21dd73d834e4844f98c2506514e1d
    <h1>QnA</h1>
    <hr />
    <form @submit="submitForm"> 
        <h2>질문하기</h2>
        <textarea name="question"></textarea> 
        <input type="submit" value="확인" /> 
    </form>
    <div>
        <div v-for="(item, index) in questionData" :key="index">
            {{ item.title }} - {{ item.content }}
        </div>
<<<<<<< HEAD
=======
<h1>QnA</h1>
<hr />
<form @submit.prevent="submitForm()">
    <h2>질문하기</h2>
    <textarea></textarea>
    <input type="submit" value="확인" />
</form>
<div>
    <div v-for="item in questionData" v-bind:key="item">
        {{ item.title }} - {{ item.content }}
>>>>>>> 088410f2d2f734197810ebbc2fb6f3199a1dbdc0
=======
>>>>>>> 6d62b3918dd21dd73d834e4844f98c2506514e1d
    </div>
</template>
