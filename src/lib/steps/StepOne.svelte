<script>
	import MovieCard from '$lib/MovieCard.svelte';
	export let handleSelectMovie;
	let query = '';
	let movies;
	let loading;

	const handleSubmit = async (e) => {
		e.preventDefault();
		loading = true;
		const url = `https://api.themoviedb.org/3/search/movie?api_key=${
			import.meta.env.VITE_TMDB_API_KEY
		}&language=en-US&query=${query}&page=1&include_adult=false`;
		try {
			const res = await fetch(url);
			const data = await res.json();
			movies = data.results;
		} catch (error) {
			console.log(error);
		} finally {
			loading = false;
			movies = movies.splice(0, 10);
		}
	};
</script>

<div>
	<form on:submit={handleSubmit}>
		<label for="query">Search Movie Name</label>
		<input class="bg-gray-400" bind:value={query} name="query" type="text" />
		<button>Search</button>
	</form>
</div>
<div class="h-96 overflow-scroll bg-gray-700 rounded p-4">
	{#if !movies && !loading}
		<h1>Search for a movie</h1>
	{:else if loading}
		<h1>Looking for your movies</h1>
	{:else if !loading && movies}
		{#each movies as movie}
			<MovieCard {handleSelectMovie} {movie} />
		{/each}
	{/if}
</div>
