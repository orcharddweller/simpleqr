<script lang="ts">
	import QRCode from 'qrcode';

	type Props = {
		text: string;
	};

	let { text }: Props = $props();

	let qrCode = $state('');

	const generateQR = async () => {
		if (!text) {
			alert('Please enter text to generate QR code');
			return;
		}

		qrCode = await QRCode.toDataURL(text);
	};
</script>

<button
	disabled={!text}
	onclick={generateQR}
	class={text
		? 'bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600'
		: 'bg-gray-300 text-gray-500 px-4 py-2 rounded cursor-not-allowed'}
>
	Generate QR Code
</button>

{#if qrCode}
	<div class="mt-4">
		<img src={qrCode} alt="QR Code" class="border rounded" />
	</div>
{/if}
