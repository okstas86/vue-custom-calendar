<template>
	<div>
		<SelectedDay
			v-if="selectedDay !== ''"
			:selectedDay="selectedDay"
			@go-back="showCalendar"
		/>
		<Calendar v-else @date-selected="dateSelected" />
	</div>
</template>
<script setup>
import Calendar from "./components/Calendar.vue"
import SelectedDay from "./components/SelectedDay.vue"
import { ref } from "vue"

const selectedDay = ref("")

function dateSelected(day) {
	selectedDay.value = day
	console.log("selectedDay.value:", selectedDay.value)
}

function showCalendar() {
	selectedDay.value = ""
}
</script>

<style scoped></style>
