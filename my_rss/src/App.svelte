<script>
	import 'bulma/css/bulma.css'
	import Feed from './Feed.svelte';
	import * as sourcesJSON from '../public/sources.json'

	let proxyCORS = sourcesJSON.proxy.url;	
	let sources = sourcesJSON.sources;
</script>

<main>

	<div class="columns">
		{#each sources as newsFeed}
			<div class="column">
				<Feed feedURL={proxyCORS + newsFeed.url} feedName={newsFeed.name}></Feed>
			</div>        
        {/each} 
	</div>
</main>

<style>
	.columns {
        margin-right: 50px; 
		margin-left: 50px; 
		margin-top: 50px;
    }
</style>

