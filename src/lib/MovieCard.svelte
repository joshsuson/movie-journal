<script>
	export let movie;
	export let handleSelectMovie;
	const imgSource = `https://image.tmdb.org/t/p/w185_and_h278_bestv2/${movie.poster_path}`;
</script>

<div
	on:click={() => handleSelectMovie(movie)}
	class="bg-gray-800 grid grid-cols-4 w-3/4 my-3 p-2 rounded mx-auto cursor-pointer border-2 border-gray-800 hover:border-indigo-600"
>
	<div class="col-span-1">
		<img class="rounded" src={imgSource} alt={`${movie.title} poster image`} />
	</div>
	<div class="col-span-3">
		<h2
			class="text-3xl inline-block uppercase bg-gradient-to-r from-green-400 via-blue-500 to-indigo-600 mb-2"
		>
			{movie.title}
		</h2>
		<h3 class="text-gray-500 mb-2">{movie.release_date}</h3>
		<p class="leading-relaxed text-gray-300">{movie.overview}</p>
	</div>
</div>

<style>
	h2 {
		background-position: 0px 88%;
		background-size: 100% 0.2em;
		background-repeat: no-repeat;
	}
</style>
