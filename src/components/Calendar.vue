<template>
	<div class="calendar">
		<div class="language-switcher">
			<button @click="switchLanguage('ru')">RU</button>
			<button @click="switchLanguage('en')">EN</button>
		</div>
		<div class="header">
			<button @click="prevMonth">&lt;</button>
			<h2>{{ currentMonthName }}</h2>
			<button @click="nextMonth">&gt;</button>
		</div>
		<div class="days-grid">
			<div
				class="day"
				v-for="dayOfWeek in languages[currentLanguage].days"
				:key="dayOfWeek"
			>
				{{ dayOfWeek }}
			</div>
			<div v-for="day in days" :key="day" class="day" @click="selectDate(day)">
				{{ day }}
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			currentDate: new Date(),
			currentLanguage: "ru",
			languages: {
				ru: {
					months: [
						"Январь",
						"Февраль",
						"Март",
						"Апрель",
						"Май",
						"Июнь",
						"Июль",
						"Август",
						"Сентябрь",
						"Октябрь",
						"Ноябрь",
						"Декабрь",
					],
					days: ["Вс", "Пн", "Вт", "Ср", "Чт", "Пт", "Сб"],
				},
				en: {
					months: [
						"January",
						"February",
						"March",
						"April",
						"May",
						"June",
						"July",
						"August",
						"September",
						"October",
						"November",
						"December",
					],
					days: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
				},
			},
		}
	},
	computed: {
		currentMonthName() {
			return this.languages[this.currentLanguage].months[
				this.currentDate.getMonth()
			]
		},
		days() {
			const daysInMonth = new Date(
				this.currentDate.getFullYear(),
				this.currentDate.getMonth() + 1,
				0
			).getDate()
			const firstDayIndex = new Date(
				this.currentDate.getFullYear(),
				this.currentDate.getMonth(),
				1
			).getDay()
			const days = []

			for (let i = 1; i <= daysInMonth; i++) {
				days.push(i)
			}

			for (let i = 0; i < firstDayIndex; i++) {
				days.unshift("")
			}

			return days
		},
	},
	methods: {
		prevMonth() {
			const prevMonthDate = new Date(this.currentDate)
			prevMonthDate.setMonth(prevMonthDate.getMonth() - 1)
			this.currentDate = prevMonthDate
		},
		nextMonth() {
			const nextMonthDate = new Date(this.currentDate)
			nextMonthDate.setMonth(nextMonthDate.getMonth() + 1)
			this.currentDate = nextMonthDate
		},
		selectDate(day) {
			if (day !== "") {
				const selectedDate = new Date(
					this.currentDate.getFullYear(),
					this.currentDate.getMonth(),
					day
				)

				const selectedDateTime = {
					year: selectedDate.getFullYear(),
					month: selectedDate.getMonth(),
					day: selectedDate.getDate(),
					hour: new Date().getHours(),
					minute: new Date().getMinutes(),
				}

				this.$emit("date-selected", selectedDateTime)
			}
		},

		switchLanguage(language) {
			this.currentLanguage = language
		},
	},
}
</script>

<style scoped>
.calendar {
	width: 300px;
	font-family: Arial, sans-serif;
}

.language-switcher {
	margin-bottom: 10px;
}

.language-switcher button {
	margin-right: 5px;
	padding: 5px 10px;
	border: none;
	background-color: #f0f0f0;
	cursor: pointer;
}

.header {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin-bottom: 10px;
}

.header button {
	padding: 5px 10px;
	border: none;
	background-color: #f0f0f0;
	cursor: pointer;
}

.days-grid {
	display: grid;
	grid-template-columns: repeat(7, 1fr);
	gap: 5px;
}

.day {
	padding: 5px;
	text-align: center;
	background-color: #f0f0f0;
	cursor: pointer;
}

.day:hover {
	background-color: #dcdcdc;
}
</style>
