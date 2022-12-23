<script lang="ts">
	let username = '';
	let password = '';
	let basic = 'Basic ...';
	let copied = false;

	$: {
		if (username && password) {
			const base64 = window.btoa(`${username}:${password}`);
			basic = 'Basic ' + base64;
		} else {
			basic = 'Basic ...';
		}
	}

	$: copyText = copied ? 'Copied to clipboard ✓' : 'Copy to clipboard.';

	function copyToClipboard() {
		copied = true;
		navigator.clipboard.writeText(basic);
	}
</script>

<div class="h-1/2 w-screen grid place-items-center">
	<div class="w-1/2 h-2/3 border-4 border-gray-600 bg-gray-200 rounded-xl drop-shadow-xl p-12">
		<div class="flex flex-col gap-8">
			<div class="flex flex-row gap-4">
				<input
					type="text"
					bind:value={username}
					class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
					placeholder="Username"
					autocomplete="off"
					name="otp"
				/>

				<input
					type="text"
					bind:value={password}
					class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
					placeholder="Password"
					autocomplete="off"
					name="otp"
				/>
			</div>

			<div class="flex flex-row gap-4 items-center">
				<button
					type="button"
					class="tt-container relative bg-gray-300 rounded-lg text-sm h-10 w-10 grid place-items-center disabled:pointer-events-none"
					on:click={copyToClipboard}
					disabled={basic === 'Basic ...'}
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						viewBox="0 0 384 512"
						class="w-7 h-5 text-gray-600 hover:text-gray-400 disabled:text-gray-300 active:text-blue-300"
						fill="currentColor"
						><path
							d="M384 96L384 0h-112c-26.51 0-48 21.49-48 48v288c0 26.51 21.49 48 48 48H464c26.51 0 48-21.49 48-48V128h-95.1C398.4 128 384 113.6 384 96zM416 0v96h96L416 0zM192 352V128h-144c-26.51 0-48 21.49-48 48v288c0 26.51 21.49 48 48 48h192c26.51 0 48-21.49 48-48L288 416h-32C220.7 416 192 387.3 192 352z"
						/></svg
					>
					<span
						class="tt-text bg-gray-800 text-white absolute p-3 rounded-md -left-1/2 top-full w-32 pointer-events-none"
						class:text-green-400={copied}>{copyText}</span
					>
				</button>

				<p class="text-4xl font-extrabold text-gray-900 select-none">
					{basic}
				</p>
			</div>
		</div>
	</div>
</div>

<style lang="scss">
	.tt-container .tt-text {
		visibility: hidden;
	}

	.tt-container:hover .tt-text {
		visibility: visible;
	}
</style>
