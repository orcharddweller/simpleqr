<script lang="ts">
	import Text from './(inputs)/Text.svelte';
	import Wifi from './(inputs)/Wifi.svelte';
	import Generator from './Generator.svelte';

	let currentTab = $state(0);

	let text = $state('');

	const inputs = [
		{
			name: 'Text',
			snippet: textInput
		},
		{
			name: 'Wi-Fi',
			snippet: wifiInput
		}
	];

	const currentSnippet = $derived(inputs[currentTab].snippet);
</script>

{#snippet textInput()}
	<Text bind:text />
{/snippet}

{#snippet wifiInput()}
	<Wifi bind:text />
{/snippet}

<main class="container mx-auto p-4">
	<h1 class="text-2xl font-bold mb-4">QR Code Generator</h1>

	<div role="tablist" class="tabs tabs-boxed">
		{#each inputs as { name }, i}
			<button
				role="tab"
				class={'tab' + (currentTab === i ? ' tab-active' : '')}
				onclick={() => {
					text = '';
					currentTab = i;
				}}>{name}</button
			>
		{/each}
	</div>

	<div class="m-4">
		{@render currentSnippet()}
	</div>

	<Generator {text} />
</main>
