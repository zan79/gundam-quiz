<script setup>
import { ref, computed } from 'vue'
import { onMounted } from "@vue/runtime-core";

const ques = ref([
	{//gundam
		question: 'https://m.media-amazon.com/images/W/IMAGERENDERING_521856-T1/images/I/81QdlfKVtFL.jpg',
		answer: 2,
		options: [
			'00 Gundam',
			'0 Gundam',
			'Gundam',
			'Barbatos'
		],
		selected: null
	},
	{//b
		question: 'https://m.media-amazon.com/images/W/IMAGERENDERING_521856-T1/images/I/71Al4oZqelL.jpg',
		answer: 0,
		options: [
			'Barbatos',
			'Barbatos 4th form',
			'Barbatos Lupus',
			'Barbatos Lupus Rex'
		],
		selected: null
	},
	{//bl
		question: 'https://www.toysonfire.ca/i/60173_5ab7990/gundam-iron-blooded-orphans-full-mechanics-1-100-scale-model-kit-01-gundam-barbatos-lupus-60173.jpg',
		answer: 2,
		options: [
			'Barbatos',
			'Barbatos 4th form',
			'Barbatos Lupus',
			'Barbatos Lupus Rex'
		],
		selected: null
	},
	{//blr
		question: 'https://m.media-amazon.com/images/W/IMAGERENDERING_521856-T1/images/I/61wdSTAvb7L.jpg',
		answer: 3,
		options: [
			'Barbatos',
			'Barbatos 4th form',
			'Barbatos Lupus',
			'Barbatos Lupus Rex'
		],
		selected: null
	},
	{//w
		question: 'https://m.media-amazon.com/images/W/IMAGERENDERING_521856-T1/images/I/617yY5PouwL._AC_SL1181_.jpg',
		answer: 2,
		options: [
			'Freedom Gundam',
			'Strike Freedom Gundam',
			'Wing Gundam',
			'Wing Gundam Zero'
		],
		selected: null
	},
	{//wz
		question: 'https://m.media-amazon.com/images/W/IMAGERENDERING_521856-T1/images/I/71G+kM0QlKL._AC_SL1205_.jpg',
		answer: 3,
		options: [
			'Freedom Gundam',
			'Strike Freedom Gundam',
			'Wing Gundam',
			'Wing Gundam Zero'
		],
		selected: null
	},
	{//s
		question: 'https://m.media-amazon.com/images/W/IMAGERENDERING_521856-T1/images/I/61vf8QxjMyL._AC_SL1256_.jpg',
		answer: 2,
		options: [
			'Freedom Gundam',
			'Strike Freedom Gundam',
			'Strike Gundam',
			'Turn A Gundam'
		],
		selected: null
	},
	{//f
		question: 'https://m.media-amazon.com/images/W/IMAGERENDERING_521856-T1/images/I/71Lp7moGVJL._AC_SL1500_.jpg',
		answer: 0,
		options: [
			'Freedom Gundam',
			'Strike Freedom Gundam',
			'Wing Gundam',
			'Wing Gundam 0'
		],
		selected: null
	},
	{//sf
		question: 'https://m.media-amazon.com/images/I/71IfpsZqeIL._AC_UF894,1000_QL80_.jpg',
		answer: 1,
		options: [
			'Freedom Gundam',
			'Strike Freedom Gundam',
			'Wing Gundam',
			'Wing Gundam Zero'
		],
		selected: null
	},
	{//0
		question: 'https://m.media-amazon.com/images/W/IMAGERENDERING_521856-T1/images/I/61xapO3OrPL._AC_SL1500_.jpg',
		answer: 1,
		options: [
			'Gundam',
			'0 Gundam',
			'00 Gundam',
			'Turn A Gundam'
		],
		selected: null
	},
	{//00
		question: 'https://m.media-amazon.com/images/W/IMAGERENDERING_521856-T1/images/I/61lLuz4PWGL.jpg',
		answer: 2,
		options: [
			'Turn A Gundam',
			'0 Gundam',
			'00 Gundam',
			'Gundam 00 Qan[T]'
		],
		selected: null
	},
	{//00q
		question: 'https://m.media-amazon.com/images/W/IMAGERENDERING_521856-T1/images/I/51q58BqbclL._AC_SY450_.jpg',
		answer: 3,
		options: [
			'Turn A Gundam',
			'0 Gundam',
			'00 Gundam',
			'Gundam 00 Qan[T]'
		],
		selected: null
	},
	{//00q
		question: 'https://m.media-amazon.com/images/W/IMAGERENDERING_521856-T1/images/I/71AUiPvIO1L._AC_SY606_.jpg',
		answer: 0,
		options: [
			'Turn A Gundam',
			'0 Gundam',
			'00 Gundam',
			'Gundam 00 Qan[T]'
		],
		selected: null
	},
	{//nu
		question: 'https://i.ebayimg.com/images/g/WT8AAOSwaMNjgcOD/s-l1600.png',
		answer: 0,
		options: [
			'Turn A Gundam',
			'Gundam',
			'Nu Gundam',
			'Gundam F91'
		],
		selected: null
	},
	{//f91
		question: 'https://d3nt9em9l1urz8.cloudfront.net/media/catalog/product/cache/3/image/9df78eab33525d08d6e5fb8d27136e95/b/i/bibas61067-1.jpg',
		answer: 0,
		options: [
			'Turn A Gundam',
			'Gundam',
			'Nu Gundam',
			'Gundam F91'
		],
		selected: null
	},
])

const quizCompleted = ref(false)
const quizStart = ref(false)
const currentQuestion = ref(0)
const questions = ref([])
const score = computed(() => {
	let value = 0
	questions.value.map(q => {
		if (q.selected != null && q.answer == q.selected) {
			console.log('correct');
			value++
		}
	})
	return value
})

const getCurrentQuestion = computed(() => {
	let question = questions.value[currentQuestion.value]
	question.index = currentQuestion.value
	return question
})

const getCindex = computed(() => {
	let question = questions.value[currentQuestion.value]
	// question.index = currentQuestion.value
	return question.index
})

const SetAnswer = (e) => {
	questions.value[currentQuestion.value].selected = e.target.value
	e.target.value = null
}

const NextQuestion = () => {
	if (currentQuestion.value < questions.value.length - 1) {
		currentQuestion.value++
		return
	}

	quizCompleted.value = true
}

const TryAgain = () => {
	location.reload();
}
const StartQuiz = () => {
	quizStart.value = true;
	randomize()
}
const randomize = async () => {
	console.log("dawd")
  for (let i = ques.value.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        const temp = ques.value[i];
        ques.value[i] = ques.value[j];
        ques.value[j] = temp;
        questions.value = ques.value.slice(0, 10);
    }
}

onMounted(() => {
	randomize()
	quizStart.value = true;
})
</script>

<template>
	<main class="app">
		<h1>Name The Gundam</h1>
		<section v-if="!quizStart">
			<div>
				<br>
				<br>
				<br>
				<br>
				<br>
				<h2>Multiple choice, select the correct name of the Gundam</h2>
				<br>
				<br>
				<br>
				<br>
				<br>
			</div>
			<div class="option" @click="StartQuiz">
				<h3>Start</h3>
			</div>
		</section>

		<section class="quiz" v-else-if="!quizCompleted">
			<img v-bind:src="getCurrentQuestion.question" alt="">
			<!-- <div class="quiz-info">
				<span class="score">{{ getCindex+1 }}/{{ questions.length }}</span>
			</div> -->
			<p class="score">{{ getCindex+1 }}/{{ questions.length }}</p>

			<div class="options">
				<label v-for="(option, index) in getCurrentQuestion.options" :for="'option' + index" :class="`option ${getCurrentQuestion.selected == index
						? index == getCurrentQuestion.answer
							? 'correct'
							: 'wrong'
						: ''
					} ${getCurrentQuestion.selected != null &&
						index != getCurrentQuestion.selected
						? 'disabled'
						: ''
					}`">
					<input type="radio" :id="'option' + index" :name="getCurrentQuestion.index" :value="index"
						v-model="getCurrentQuestion.selected" :disabled="getCurrentQuestion.selected" @change="SetAnswer" />
					<span>{{ option }}</span>
				</label>
			</div>

			<button @click="NextQuestion" :disabled="!getCurrentQuestion.selected">
				{{
					getCurrentQuestion.index == questions.length - 1
					? 'Finish'
					: getCurrentQuestion.selected == null
						? ''
						: 'Next'
				}}
			</button>
		</section>

		<section v-else-if="quizCompleted">
			<h2>You have finished the quiz!</h2>
			<h1>Your score is {{ score }}/{{ questions.length }}</h1>
			<div>
				<br>
				<br>
				<br>
				<br>
				<br>
				<br>
				<br>
				<br>
				<br>
				<br>
				<br>
			</div>
			<div class="option" @click="TryAgain">
				<h3>Try Again </h3>
			</div>
		</section>
	</main>
</template>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: 'Montserrat', sans-serif;
}

body {
	background-color: #ffffff;
	color: #FFF;
}

.app {
	display: flex;
	flex-direction: column;
	align-items: center;
	padding: 2rem;
	height: 100vh;
}

h1 {
	font-size: 2rem;
	color: #2b45bd;
	text-align: center;
}

h3 {
	text-align: center;
	margin: 0;
	padding: 0;
}

.quiz {
	background-color: #ffffff;
	padding: 1rem;
	padding-top: 0.3rem;
	width: 100%;
	max-width: 640px;
}

.quiz-info {
	display: flex;
	justify-content: space-between;
	margin-bottom: 1rem;
}

.quiz-info .question {
	color: #000000;
	font-size: 1.25rem;
}

.quiz-info .score {
	color: #000000;
	font-size: 1.25rem;
}

.options {
	margin-bottom: 1rem;
}

/* label{
	font-size: 0.5rem;
	margin: 0;
	padding: 0;
} */
.option {
	padding: 0.6rem;
	display: block;
	background-color: #2b45bd;
	margin-bottom: 0.5rem;
	border-radius: 0.5rem;
	cursor: pointer;
}


.option.correct {
	background-color: #03924b;
}

.option.wrong {
	background-color: #ff0008;
}

.option:last-of-type {
	margin-bottom: 0;
}

.option.disabled {
	opacity: 0.2;
	color: #ffffff;
	background: #000000;
}

.option input {
	display: none;
}

button {
	appearance: none;
	outline: none;
	border: none;
	cursor: pointer;
	padding: 0.5rem 1rem;
	background-color: rgb(255, 255, 26);
	color: #000000;
	font-weight: 700;
	text-transform: uppercase;
	font-size: 1.2rem;
	border-radius: 0.5rem;
	text-align: center;
	float: right;
}

button:disabled {
	opacity: 0.1;
	background: #ffffff;
	color: white;
}

h2 {
	font-size: 2rem;
	margin-bottom: 2rem;
	margin-top: 5rem;
	text-align: center;
	color: #ff0008;
}

p {
	color: #000000;
	font-size: 1.5rem;
	text-align: center;
}

span {
	text-align: center;
}

img {
	object-fit: scale-down;
	width: 280px;
	height: 300px;
	/* border: 1px solid #666; */
}
</style>
