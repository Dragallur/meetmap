<script>
	import Date from "./lib/Date.svelte";
	import Calendar from "./lib/Calendar.svelte";
	import Schedule from "./lib/Schedule.svelte";

	let arr_clicked_days = [];
	let selected_times = {};
	function day_clicked(event) {
		if (arr_clicked_days.includes(event.detail.day)) {
			arr_clicked_days = arr_clicked_days.filter(
				(day) => day !== event.detail.day,
			);
			const dateString = event.detail.day.toISOString().split("T")[0];
			delete selected_times[dateString];
			selected_times = { ...selected_times }; // Trigger reactivity
		} else {
			arr_clicked_days.push(event.detail.day);
		}
		arr_clicked_days = arr_clicked_days;
		arr_clicked_days.sort(function (a, b) {
			return a - b;
		});
		console.log(arr_clicked_days);
	}

	function tile_times_clicked(event) {
		const { day, hour } = event.detail;
		const dateString = day.toISOString().split("T")[0];
		if (!selected_times[dateString]) {
			selected_times[dateString] = [];
		}

		const index = selected_times[dateString].indexOf(hour);
		if (index > -1) {
			selected_times[dateString].splice(index, 1);
		} else {
			selected_times[dateString].push(hour);
		}

		selected_times = { ...selected_times }; // Trigger reactivity
		console.log(selected_times);
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
			{selected_times}
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
