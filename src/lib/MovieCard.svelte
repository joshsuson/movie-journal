<script>
	export let movie;
	export let handleSelectMovie;
	const imgSource = `https://image.tmdb.org/t/p/w185_and_h278_bestv2/${movie.poster_path}`;
</script>

<div on:click={() => handleSelectMovie(movie)}>
	<img src={imgSource} alt={`${movie.title} poster image`} />
	<h2>{movie.title}</h2>
	<h3>{movie.release_date}</h3>
	<p>{movie.overview}</p>
</div>
