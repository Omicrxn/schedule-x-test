<script lang="ts">
	import { browser } from '$app/environment';
	import type { CalendarEventExternal } from '@schedule-x/calendar';

	let { calendarEvent }: { calendarEvent: CalendarEventExternal } = $props();
</script>

{#if calendarEvent}
	<div class="flex flex-col gap-2">
		<p>
			{calendarEvent.title}
		</p>
		<!-- Uncomment this and it will stop working -->
		<!-- <p>
			{calendarEvent.start}
		</p> -->
	</div>
{/if}
