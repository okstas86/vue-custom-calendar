<template>
	<div class="selected-day">
		<div class="data-item">
			<span class="label">Год:</span>
			<span class="value">{{ selectedDay.year }}</span>
		</div>
		<div class="data-item">
			<span class="label">Месяц:</span>
			<span class="value">{{ selectedDay.month }}</span>
		</div>
		<div class="data-item">
			<span class="label">День:</span>
			<span class="value">{{ selectedDay.day }}</span>
		</div>
		<div class="data-item">
			<span class="label">Часы:</span>
			<span class="value">{{ selectedDay.hour }}</span>
		</div>
		<div class="data-item">
			<span class="label">Минуты:</span>
			<span class="value">{{ selectedDay.minute }}</span>
		</div>

		<button @click="goBack">Вернуться к календарю</button>
	</div>
</template>

<script setup>
const { selectedDay } = defineProps(["selectedDay"])
const emit = defineEmits(["go-back"])

const goBack = () => {
	emit("go-back")
}
</script>

<style scoped>
.selected-day {
	text-align: center;
	padding: 20px;
}

.data-item {
	margin-bottom: 10px;
}

.label {
	font-weight: bold;
	margin-right: 5px;
}

.value {
	color: #007bff;
}

button {
	margin-top: 20px;
	padding: 10px 20px;
	background-color: #007bff;
	color: #fff;
	border: none;
	border-radius: 5px;
	cursor: pointer;
}

button:hover {
	background-color: #0056b3;
}
</style>
