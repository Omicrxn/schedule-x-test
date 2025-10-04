<script lang="ts">
	import { ScheduleXCalendar } from '@schedule-x/svelte';
	import {
		CalendarApp,
		createCalendar,
		createViewDay,
		createViewMonthGrid,
		createViewWeek
	} from '@schedule-x/calendar';
	import '@schedule-x/theme-default/dist/index.css';
	import 'temporal-polyfill/global';
	import { createEventsServicePlugin } from '@schedule-x/events-service';
	import { onMount } from 'svelte';
	import { createEventModalPlugin } from '@schedule-x/event-modal';
	import EventModal from './event-modal.svelte';

	const eventModal = createEventModalPlugin();
	const eventsServicePlugin = createEventsServicePlugin();

	let calendarApp = $state<CalendarApp>();
	$effect.pre(() => {
		calendarApp = createCalendar({
			plugins: [eventModal, eventsServicePlugin],
			views: [createViewDay(), createViewWeek(), createViewMonthGrid()],
			defaultView: 'month-grid',
			events: [
				{
					id: '1',
					title: 'Event 1',
					start: Temporal.PlainDate.from('2025-10-04'),
					end: Temporal.PlainDate.from('2025-10-04')
				},
				{
					id: '2',
					title: 'Event 2',
					start: Temporal.ZonedDateTime.from('2025-10-03T02:00:00+09:00[Asia/Tokyo]'),
					end: Temporal.ZonedDateTime.from('2025-10-03T04:00:00+09:00[Asia/Tokyo]')
				}
			]
		});
	});
</script>

<div>
	<ScheduleXCalendar calendarApp={calendarApp!} eventModal={EventModal} />
	<button
		onclick={() => {
			calendarApp?.eventsService.add({
				title: 'Event 1',
				start: Temporal.PlainDate.from('2025-10-20'),
				end: Temporal.PlainDate.from('2025-10-20'),
				id: 1
			});
		}}
	>
		Add Event
	</button>
</div>
