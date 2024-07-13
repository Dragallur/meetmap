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
		console.log(arr_clicked_days);
	}

	let arr_clicked_tile_times = [];
	function tile_times_clicked(event) {
		if (arr_clicked_tile_times.includes(event.detail.day_hour)) {
			arr_clicked_tile_times = arr_clicked_tile_times.filter(
				(day_hour) => day_hour !== event.detail.day_hour,
			);
		} else {
			arr_clicked_tile_times.push(event.detail.day_hour);
			arr_clicked_tile_times = arr_clicked_tile_times;
		}
		arr_clicked_tile_times.sort(function (a, b) {
			if (a[0] === b[0]) {
				return a[1] - b[1];
			} else {
				return a[0] - b[0];
			}
		});
		console.log(arr_clicked_tile_times.map((subArray) => subArray[1]));
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
		<Schedule
			on:tile_times_clicked={tile_times_clicked}
			{arr_clicked_days}
		/>
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
