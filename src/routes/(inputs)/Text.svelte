<script lang="ts">
	import type { InputProps } from '$lib/types';

	let { text = $bindable() }: InputProps = $props();
</script>

<div class="mb-4">
	<input
		type="text"
		bind:value={text}
		placeholder="Enter text or message"
		class="w-full p-2 border rounded"
	/>
</div>
