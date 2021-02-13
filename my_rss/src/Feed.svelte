<script>
    import News from './News.svelte';
    import { onMount } from 'svelte';

    export let feedName;
    export let feedURL;

    // Taken from https://cors-anywhere.herokuapp.com/corsdemo
    
    let newsFeed = [];

    onMount(async () => {
		const res = await fetch(feedURL)
        .then(response => response.text())
        .then(str => (new window.DOMParser()).parseFromString(str, "text/xml"));

        let items = res.getElementsByTagName("item");//.getElementsByTagName("title")[0].textContent;

        let toDisplay = []
        for (var i = 0; i < items.length; i++) {   
            let item = items[i];
            let title = item.getElementsByTagName("title")[0].textContent;
            let description = item.getElementsByTagName("description")[0].textContent;
            let linkArticle = item.getElementsByTagName("link")[0].textContent;
            let pubDate = item.getElementsByTagName("pubDate")[0].textContent.slice(0, -5);

            toDisplay = [...toDisplay, {title,description,linkArticle, pubDate}];
        }   
        newsFeed = toDisplay;
    });
    
    
</script>

<main>
    <div class="container is-max-desktop">
        <div class="notification is-light">
            <div class="container">
                <p><b>{feedName}</b></p>
            </div>
            <div class="container">
                {#await newsFeed}
                    <p>...waiting</p>
                {:then response}
                    {#each response as {title, description, linkArticle, pubDate}}
                        <News title={title} description={description} linkArticle={linkArticle} pubDate={pubDate}></News>
                    {/each}    
                {:catch error}
                    <p style="color: red">{error.message}</p>
                {/await}
            </div>
            
        </div>
    </div>
</main>

<style>
	
</style>