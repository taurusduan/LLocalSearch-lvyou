<script lang="ts">
	import { draw } from 'svelte/transition';
	export let sendMode: boolean;
	export let prompt: string;
	export let sendPrompt: () => void;
	export let resetChat: () => void;

	export let eventSource: EventSource | null;
	export let stopChat: () => void;
</script>

<div
	class="text-stone-500 hover:text-stone-700 rounded-2xl hover:cursor-pointer transition-all dark:text-stone-500 dark:hover:text-stone-200"
>
	{#if sendMode && prompt != ''}
		<span title="send message">
			<button
				class="bg-stone-200 text-stone-500 hover:text-stone-700 hover:cursor-pointer hover:bg-stone-300 m-1 p-1 transition-all rounded-xl w-8 h-8 dark:bg-stone-700 dark:text-stone-400 dark:hover:bg-stone-600 dark:hover:text-stone-300 hover:shadow-inner"
				on:click={() => {
					sendPrompt();
				}}
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					viewBox="0 0 24 24"
					stroke-width="1.5"
					stroke="currentColor"
					class="w-6 h-6"
				>
					<path
						in:draw={{ duration: 500 }}
						stroke-linecap="round"
						stroke-linejoin="round"
						d="M6 12 3.269 3.125A59.769 59.769 0 0 1 21.485 12 59.768 59.768 0 0 1 3.27 20.875L5.999 12Zm0 0h7.5"
					/>
				</svg>
			</button>
		</span>
	{:else if !sendMode && eventSource}
		<span title="stop chat">
			<button
				class="bg-stone-200 text-stone-500 hover:text-stone-700 hover:cursor-pointer hover:bg-stone-300 m-1 p-1 transition-all rounded-xl w-8 h-8 dark:bg-stone-700 dark:text-stone-400 dark:hover:bg-stone-600 dark:hover:text-stone-300"
				on:click={() => {
					stopChat();
					sendMode = true;
				}}
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					viewBox="0 0 24 24"
					stroke-width="1.5"
					stroke="currentColor"
					class="w-6 h-6"
				>
					<path
						in:draw={{ duration: 500 }}
						stroke-linecap="round"
						stroke-linejoin="round"
						d="M5.25 7.5A2.25 2.25 0 0 1 7.5 5.25h9a2.25 2.25 0 0 1 2.25 2.25v9a2.25 2.25 0 0 1-2.25 2.25h-9a2.25 2.25 0 0 1-2.25-2.25v-9Z"
					/>
				</svg>
			</button>
		</span>
	{:else}
		<span title="reset chat">
			<button
				class="bg-stone-200 text-stone-500 hover:text-stone-700 hover:cursor-pointer hover:bg-stone-300 m-1 p-1 transition-all rounded-xl w-8 h-8 dark:bg-stone-700 dark:text-stone-400 dark:hover:bg-stone-600 dark:hover:text-stone-300"
				on:click={() => {
					resetChat();
					sendMode = true;
				}}
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					fill="none"
					viewBox="0 0 24 24"
					stroke-width="1.5"
					stroke="currentColor"
					class="w-6 h-6"
				>
					<path
						in:draw={{ duration: 500 }}
						stroke-linecap="round"
						stroke-linejoin="round"
						d="M9 15 3 9m0 0 6-6M3 9h12a6 6 0 0 1 0 12h-3"
					/>
				</svg>
			</button>
		</span>
	{/if}
</div>
