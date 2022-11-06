<script>
	import { onMount } from 'svelte';
	import axios from 'axios';
	import chevronDoubleUp from '$lib/images/chevron-double-up.svg';
	import chevronDoubleDown from '$lib/images/chevron-double-down.svg';
	import chatBubleBottomCenter from '$lib/images/chat-bubble-bottom-center.svg';

	let children = [];

	onMount(async () => {
		try {
			const { data } = await axios.get('https://www.reddit.com/r/javascript.json');

			children = data.data.children;

			console.log(children);
		} catch (error) {
			console.log(error);
		}
	});
</script>

<div class="flex justify-center my-8">
	<ul>
		{#each children as post}
			<li class="p-2 flex items-center">
				<div class="mr-2">
					<img src={chevronDoubleUp} class="w-4" />
					<div class="flex justify-center">
						{post.data.score}
					</div>
					<img src={chevronDoubleDown} class="w-4" />

					<div class="flex" />
				</div>

				<div class="flex">
					<a href={post.data.url} class="font-bold ml-2">{post.data.title}</a>
					<div class="ml-2 flex justify-end text-gray-500">
						<img src={chatBubleBottomCenter} class="w-4 mr-1" />
						{post.data.num_comments}
					</div>
				</div>
			</li>
		{/each}
	</ul>
</div>
