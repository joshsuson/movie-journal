<script>
	import MovieCard from '$lib/MovieCard.svelte';

	export let handleSelectMovie;
	export let selectedMovie
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
			console.log(movies);
		}
	};
</script>

<div class='my-12'>
	<form class='w-full text-center' on:submit={handleSubmit}>
		<label
			class='block mx-auto w-max mb-4 uppercase text-3xl bg-gradient-to-r from-green-400 via-blue-500 to-indigo-600 bg-clip-text text-transparent'
			for='query'>Search Movie Name</label>
		<input class='px-4 text-gray-900 text-lg bg-gray-400 rounded-tl-md rounded-bl-md h-10 w-9/12' bind:value={query}
					 name='query' type='text' />
		<button
			class='-ml-1.5 bg-gradient-to-r from-green-400 via-blue-500 to-indigo-600 h-10 inline-block w-2/12 rounded-r-md uppercase text-lg text-gray-100'>
			Search
		</button>
	</form>
</div>
<div>
	{#if !movies && !loading}
		<h1 class='text-center uppercase text-4xl text-gray-400'>Search for a movie</h1>
	{:else if loading}
		<div class='loader'>Looking for your movies</div>
	{:else if !loading && movies}
		{#if movies.length === 0}
			<div>
				<h1 class='text-center uppercase text-4xl text-gray-400'>We couldn't find your movie. Please try a different search term.</h1>
			</div>
		{:else}
			{#each movies as movie}
				<MovieCard {handleSelectMovie} {movie} {selectedMovie} />
			{/each}
		{/if}

	{/if}
</div>

<style>
    input:focus-visible {
        border: 1px solid white;
        border-right: none;
        outline: none;
    }

    .loader,
    .loader:before,
    .loader:after {
        border-radius: 50%;
        width: 2.5em;
        height: 2.5em;
        -webkit-animation-fill-mode: both;
        animation-fill-mode: both;
        -webkit-animation: load7 1.8s infinite ease-in-out;
        animation: load7 1.8s infinite ease-in-out;
    }
    .loader {
        color: #4b4fe8;
        font-size: 10px;
        margin: 80px auto;
        position: relative;
        text-indent: -9999em;
        -webkit-transform: translateZ(0);
        -ms-transform: translateZ(0);
        transform: translateZ(0);
        -webkit-animation-delay: -0.16s;
        animation-delay: -0.16s;
    }
    .loader:before,
    .loader:after {
        content: '';
        position: absolute;
        top: 0;
    }
    .loader:before {
        left: -3.5em;
        -webkit-animation-delay: -0.32s;
        animation-delay: -0.32s;
    }
    .loader:after {
        left: 3.5em;
    }
    @-webkit-keyframes load7 {
        0%,
        80%,
        100% {
            box-shadow: 0 2.5em 0 -1.3em;
        }
        40% {
            box-shadow: 0 2.5em 0 0;
        }
    }
    @keyframes load7 {
        0%,
        80%,
        100% {
            box-shadow: 0 2.5em 0 -1.3em;
        }
        40% {
            box-shadow: 0 2.5em 0 0;
        }
    }
</style>
