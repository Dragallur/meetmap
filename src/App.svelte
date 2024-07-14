<script>
	import TryDate from "./lib/TryDate.svelte";
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
			selected_times = { ...selected_times };
		} else {
			arr_clicked_days.push(event.detail.day);
		}
		arr_clicked_days = arr_clicked_days;
		arr_clicked_days.sort(function (a, b) {
			return a - b;
		});
	}

	function tile_times_clicked(event) {
		return;
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

		selected_times = { ...selected_times };
	}

	function select_range(select_origin, select_target) {
		function hasDate(dateArray, targetDate) {
			const targetTime = targetDate.getTime();
			return dateArray.some((date) => date.getTime() === targetTime);
		}
		let range_hours = [];
		const min_hours = Math.min(select_origin.hour, select_target.hour);
		const max_hours = Math.max(select_origin.hour, select_target.hour);
		for (let i = min_hours; i <= max_hours; i++) {
			range_hours.push(i);
		}
		let ordered_days = [select_origin.day, select_target.day];
		ordered_days.sort(function (a, b) {
			return a - b;
		});
		let diff_days =
			(ordered_days[1] - ordered_days[0]) / (1000 * 60 * 60 * 24);
		let range_days = [];
		for (let i = 0; i <= diff_days; i++) {
			let new_day = new Date(ordered_days[0]);
			new_day.setDate(ordered_days[0].getDate() + i);
			range_days.push(new_day);
		}
		range_days.forEach((day) => {
			const dateString = day.toISOString().split("T")[0];
			if (!hasDate(arr_clicked_days, day)) {
				return;
			}
			if (!selected_times[dateString]) {
				selected_times[dateString] = [];
			}
			range_hours.forEach((hour) => {
				const index = selected_times[dateString].indexOf(hour);
				if (is_origin_selected) {
					if (index !== -1) {
						selected_times[dateString].splice(index, 1);
					}
				} else {
					if (
						index === -1 &&
						!selected_times[dateString].includes(hour)
					) {
						selected_times[dateString].push(hour);
					}
					if (
						select_origin.day.getTime() ===
							select_target.day.getTime() &&
						select_origin.hour === select_target.hour &&
						!selected_times[dateString].includes(hour)
					) {
						selected_times[dateString].push(hour);
					}
				}
			});
			if (selected_times[dateString].length === 0) {
				delete selected_times[dateString];
			}
		});
		selected_times = { ...selected_times };
	}

	let select_origin = null;
	let is_origin_selected = false;
	let select_target = null;
	function select_from_here(event) {
		const { day, hour } = event.detail;
		select_origin = { day, hour };
		const originDateString = select_origin.day.toISOString().split("T")[0];
		is_origin_selected =
			selected_times[originDateString] &&
			selected_times[originDateString].includes(select_origin.hour);
	}

	function select_to_here(event) {
		if (select_origin == null) {
			return;
		}
		const { day, hour } = event.detail;
		select_target = { day, hour };
		select_range(select_origin, select_target);
	}

	function left_schedule(event) {
		select_origin = null;
		select_target = null;
	}
	function mouse_up(event) {
		select_origin = null;
		select_target = null;
	}
</script>

<main>
	<h1>Meetmap</h1>

	<div class="card">
		<TryDate />
	</div>

	<p>Choose date</p>

	<div class="calendar_container">
		<Calendar on:day_clicked={day_clicked} />
	</div>

	<div class="card">
		<Schedule
			on:select_from_here={select_from_here}
			on:select_to_here={select_to_here}
			on:left_schedule={left_schedule}
			on:mouse_up={mouse_up}
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
		font-family: Arial, sans-serif;
	}
</style>
