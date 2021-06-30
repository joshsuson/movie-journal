<script>
	import '../tailwind.css';
	import Icon from 'svelte-awesome';
	import { faVideo } from '@fortawesome/free-solid-svg-icons';
</script>

<header class="py-4">
	<h1 class="text-5xl flex items-center justify-center">
		<span
			class="bg-gradient-to-br from-green-400 via-blue-500 to-indigo-600 p-3 rounded-lg flex items-center justify-center"
			><Icon scale="3" data={faVideo} /></span
		>
		<span class="ml-4"> Josh Watches Movies </span>
	</h1>
</header>
<main class="max-w-6xl p-4 mx-auto">
	<slot />
</main>
<footer>
	<p>© Copyright 2021</p>
</footer>

<style>
	:global(body) {
		@apply bg-gray-900 text-gray-200;
	}
</style>
