<script>
	export let movieID;
	async function getMovie() {
		const url = `https://api.themoviedb.org/3/movie/${movieID}?api_key=${
			import.meta.env.VITE_TMDB_API_KEY
		}&language=en-US`;
		const res = await fetch(url);
		const data = await res.json();
		return data;
	}

	let movie = getMovie();
</script>

{#await movie}
	<h1>Loading your movie</h1>
{:then movie}
	<div>
		<h1>{movie.title}</h1>
	</div>
{/await}
