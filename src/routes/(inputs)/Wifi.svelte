<script lang="ts">
	import type { InputProps } from '$lib/types';

	let { text = $bindable() }: InputProps = $props();

	let ssid = $state('');
	let password = $state('');
	let encryption = $state('WPA');

	const encryptionTypes = ['None', 'WEP', 'WPA', 'WPA2'];

	$effect(() => {
		// WIFI:S:<SSID>;T:<WEP|WPA|blank>;P:<PASSWORD>;;
		text = `WIFI:S:${ssid};T:${encryption === 'None' ? '' : encryption};P:${password};;`;
	});
</script>

<div class="space-y-4">
	<input
		type="text"
		bind:value={ssid}
		placeholder="Network name (SSID)"
		class="w-full p-2 border rounded"
	/>

	<input
		type="password"
		bind:value={password}
		placeholder="Password"
		class="w-full p-2 border rounded"
	/>

	<select bind:value={encryption} class="w-full p-2 border rounded">
		{#each encryptionTypes as type}
			<option value={type}>{type}</option>
		{/each}
	</select>
</div>
