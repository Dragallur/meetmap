<script>
	import Date from "./lib/Date.svelte";
	import Calendar from "./lib/Calendar.svelte";
	import Schedule from "./lib/Schedule.svelte";

	let arr_clicked_days = [];
	function day_clicked(event) {
		if (arr_clicked_days.includes(event.detail.day)) {
			arr_clicked_days = arr_clicked_days.filter(
				(day) => day !== event.detail.day,
			);
		} else {
			arr_clicked_days.push(event.detail.day);
			arr_clicked_days = arr_clicked_days;
		}
		arr_clicked_days.sort(function (a, b) {
			return a - b;
		});
	}
</script>

<main>
	<h1>Meetmap</h1>

	<div class="card">
		<Date />
	</div>

	<p>Choose date</p>

	<div class="calendar_container">
		<Calendar on:day_clicked={day_clicked} />
	</div>

	<div class="card">
		<Schedule {arr_clicked_days} />
	</div>
</main>

<style>
	main {
		display: flex;
		flex-direction: column;
		align-items: center;
		margin: 5% 20%;
	}
</style>
