<script lang="ts">
	import type { AutocompleteOption } from '@skeletonlabs/skeleton';
	import AutocompleteWrapper from './../lib/components/AutocompleteWrapper.svelte';
	import Timeline from '$lib/components/timeline/Timeline.svelte';
	import type { ItineraryPoint } from '$lib/types/ItineraryPoint';
	import { writable } from 'svelte/store';

	const options: AutocompleteOption<string>[] = [
		{ label: 'Vanilla', value: 'vanilla', keywords: 'plain, basic', meta: { healthy: false } },
		{ label: 'Chocolate', value: 'chocolate', keywords: 'dark, white', meta: { healthy: false } },
		{ label: 'Strawberry', value: 'strawberry', keywords: 'fruit', meta: { healthy: true } },
		{
			label: 'Neapolitan',
			value: 'neapolitan',
			keywords: 'mix, strawberry, chocolate, vanilla',
			meta: { healthy: false }
		},
		{ label: 'Pineapple', value: 'pineapple', keywords: 'fruit', meta: { healthy: true } },
		{ label: 'Peach', value: 'peach', keywords: 'fruit', meta: { healthy: true } }
	];

	let inputDemo = '';

	$: points = writable<ItineraryPoint[]>([]);
</script>

<div class="w-full flex-column p-5">
	<Timeline points={$points} />

	<AutocompleteWrapper
		bind:value={inputDemo}
		{options}
		on:select={(event) => {
			$points = [
				...$points,
				{
					id: $points.length.toString(),
					name: event.detail.value.label,
					start: new Date(),
					end: new Date(),
					description:
						'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla euismod, nisl eget aliquam ultricies, nunc nisl a'
				}
			];

			console.log($points);
		}}
		on:customSelect={(event) => {
            console.log(event.detail.value);
			$points = [
				...$points,
				{
					id: $points.length.toString(),
					name: event.detail.value,
					start: new Date(),
					end: new Date(),
					description:
						'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla euismod, nisl eget aliquam ultricies, nunc nisl a'
				}
			];

			console.log($points);
		}}
	/>
</div>
