<script>
	import MusicCard from '$lib/musicCard/musicCard.svelte';
	export let data;
</script>

<div class="w-full h-full flex justify-center items-center">
	{#await Promise.all([data.streamed?.songs])}
		<div class="card h-[106px] w-[350px] animate-pulse rounded-lg">
			<div class="px-6 py-4">
				<div class="flex flex-row items-baseline justify-between">
					<div class="placeholder mb-4 h-[24px] w-1/2 rounded-lg p-0 md:h-[32px]" />
					<div class="placeholder mb-4 h-[16px] w-1/4 rounded-lg p-0 md:h-[24px]" />
				</div>
				<div class="flex flex-row items-baseline justify-between">
					<div class="placeholder h-[16px] w-1/2 rounded-lg p-0 md:h-[24px]" />
					<div class="placeholder h-[16px] w-1/4 rounded-lg p-0 md:h-[24px]" />
				</div>
			</div>
		</div>
	{:then songs}
		<!-- check if the song is currently playing or was last played -->
		{#if typeof songs[0].recenttracks.track[0]['@attr'] == 'undefined'}
			<MusicCard
				status={'Last Played'}
				song={songs[0].recenttracks.track[0].name}
				artist={songs[0].recenttracks.track[0].artist['#text']}
				songLink={songs[0].recenttracks.track[0].url}
				backgroundUrl={songs[0].recenttracks.track[0].image[3]['#text']}
			/>
		{:else}
			<MusicCard
				status={'Now Playing'}
				song={songs[0].recenttracks.track[0].name}
				artist={songs[0].recenttracks.track[0].artist['#text']}
				songLink={songs[0].recenttracks.track[0].url}
				backgroundUrl={songs[0].recenttracks.track[0].image[3]['#text']}
			/>
		{/if}
	{/await}
</div>
