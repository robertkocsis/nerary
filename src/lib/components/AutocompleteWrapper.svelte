<script lang="ts">
	import { computePosition, autoUpdate, offset, shift, flip, arrow } from '@floating-ui/dom';
	import { Autocomplete, popup } from '@skeletonlabs/skeleton';
	import type { AutocompleteOption, PopupSettings } from '@skeletonlabs/skeleton';
	import { storePopup } from '@skeletonlabs/skeleton';
	import { createEventDispatcher } from 'svelte';

	export let options: AutocompleteOption<T>[] = [];
	export let value: string = '';

	const dispatch = createEventDispatcher();

	storePopup.set({ computePosition, autoUpdate, offset, shift, flip, arrow });

	let popupSettings: PopupSettings = {
		event: 'focus-click',
		target: 'popupAutocomplete',
		placement: 'bottom'
	};
</script>

<div class="w-full flex justify-center p-5">
	<div>
		<input
			class="input"
			type="search"
			name="autocomplete"
			bind:value
			placeholder="Search..."
			use:popup={popupSettings}
			on:keypress={(event) => {
				console.log(event);
				if (event.key === 'Enter') {
					dispatch('customSelect', { value: event.target.value });
				}
			}}
		/>

		<div data-popup="popupAutocomplete" class="card p-4 overflow-y-auto" tabindex="-1">
			<Autocomplete
				bind:input={value}
				{options}
				on:selection={(event) => dispatch('select', { value: event.detail })}
				emptyState="Press enter to add a custom value..."
			/>
		</div>
	</div>
</div>
