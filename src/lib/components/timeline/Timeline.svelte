<script lang="ts">
	import type { ItineraryPoint } from '$lib/types/ItineraryPoint';

	export let points: ItineraryPoint[] = [];

	const formatDate = (date: Date) => {
		return date.toISOString();
	};

	let descriptionDisabled = false;
</script>

<ol class="border-solid border-l-4 border-surface-100 dark:border-surface-700">
	{#each points as point}
		<li class="mb-5 ms-6">
			<div class="card card-hover p-4 variant-surface rounded-xl">
				<header class="flex justify-between items-center mb-2">
					<h2 class="h2 dark:text-primary-100 text-primary-600">{point.name}</h2>

					<small class="opacity-50">{formatDate(point.start)} - {formatDate(point.end)}</small>
				</header>

				<textarea
					class="textarea opacity-60 italic bg-surface-200 dark:bg-surface-700 p-3 rounded-xl"
					placeholder="Add a description..."
					value={point.description}
					disabled={descriptionDisabled}
				></textarea>
			</div>
		</li>
	{/each}
</ol>
