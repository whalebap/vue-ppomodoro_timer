<template>
	<div class="clock">
		<div class="first_row">
			<div class="clock__hours">{{ year }}</div>
			<div class="clock__minutes">{{ month }}</div>
			<div class="clock__seconds">
				<span class="clock__hourtime">{{ day }}</span>
				<span>{{ date }}</span>
			</div>
		</div>
		<div class="second_row">
			<div class="clock__hours">
				<span class="clock__hourtime">{{ ampm }}</span>
				<span>{{ hour }}</span>
			</div>
			<div class="clock__minutes">{{ minute }}</div>
			<div class="clock__seconds">{{ second }}</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			year: "",
			month: "",
			date: "",
			day: "",
			hour: "",
			minute: "",
			second: "",
			ampm: ""
		};
	},
	mounted() {
		setInterval(this.printNow, 1000);
	},
	methods: {
		printNow() {
			const today = new Date();

			const dayNames = ["월", "화", "수", "목", "금", "토", "일"];

			(this.year = today.getFullYear()),
				(this.month = today.getMonth() + 1),
				(this.date = today.getDate()),
				(this.day = dayNames[today.getDay()]),
				(this.hour = today.getHours()),
				(this.minute = today.getMinutes()),
				(this.second = today.getSeconds()),
				(this.ampm = this.hour > 12 ? "pm" : "am");

			this.hour = this.hour % 12;
			this.hour = this.hour || 12;

			this.month = this.month < 10 ? "0" + this.month : this.month;
			this.minute = this.minute < 10 ? "0" + this.minute : this.minute;
			this.second = this.second < 10 ? "0" + this.second : this.second;
		}
	}
};
</script>

<style scoped>
.clock {
	background: #fff;
	border: 0.3rem solid #fff;
	border-radius: 0.5rem;
	display: inline-block;
	margin-bottom: 1em;
}
.first_row,
.second_row {
	margin: auto 0;
	padding: 10px;
}
.clock__hours,
.clock__minutes,
.clock__seconds {
	background: linear-gradient(to bottom, #26303b 50%, #2c3540 50%);
	display: inline-block;
	color: #fff;
	font-family: "Nunito", sans-serif;
	font-size: 3rem;
	font-weight: 300;
	padding: 0.5rem 1rem;
	text-align: center;
	position: relative;
}
.clock__hours {
	border-right: 0.15rem solid #fff;
	border-radius: 0.5rem 0 0 0.5rem;
}
.clock__minutes {
	border-right: 0.15rem solid #fff;
}
.clock__seconds {
	border-radius: 0 0.5rem 0.5rem 0;
}
.clock__hourtime {
	font-size: 1rem;
	position: absolute;
	top: 2px;
	left: 8px;
}
</style>
