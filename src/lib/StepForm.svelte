<script>
	import StepOne from './steps/StepOne.svelte';
	import StepTwo from './steps/StepTwo.svelte';
	import StepThree from './steps/StepThree.svelte';
	import StepFour from './steps/StepFour.svelte';

	let step = 1;
	let movieID;

	const handleNext = () => {
		step += 1;
	};

	const handleBack = () => {
		step -= 1;
	};

	const handleSelectMovie = (movie) => {
		movieID = movie.id;
	};
</script>

<div>
	<div class="mx-4 my-12">
		<progress class="bg-gray-50 shadow-inner rounded-3xl w-full h-6" value={step} max="4" />
	</div>
	<div>
		{#if step === 1}
			<StepOne {handleSelectMovie} />
		{:else if step === 2}
			<StepTwo {movieID} />
		{:else if step === 3}
			<StepThree />
		{:else if step === 4}
			<StepFour />
		{/if}
	</div>
	<div>
		{#if step === 1}
			<button on:click={handleNext}>Next</button>
		{:else if step === 2}
			<button on:click={handleBack}>Back</button>
			<button on:click={handleNext}>Next</button>
		{:else if step === 3}
			<button on:click={handleBack}>Back</button>
			<button on:click={handleNext}>Next</button>
		{:else if step === 4}
			<button on:click={handleBack}>Back</button>
			<button>Log</button>
		{/if}
	</div>
</div>

<style>
	progress[value]::-webkit-progress-bar {
		@apply bg-gray-50 shadow-inner;
		border-radius: 25px;
		width: 100%;
		height: 25px;
	}

	progress[value]::-webkit-progress-value {
		@apply bg-gradient-to-r from-green-400 via-blue-500 to-indigo-600;
		border-radius: 25px;
	}

	progress[value]::-moz-progress-bar {
		@apply bg-blue-400;
	}
</style>
