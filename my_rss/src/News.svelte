<script>
    export let title;
    export let description;
    export let linkArticle;
    export let pubDate;
</script>

<main>
	<div class="box">
        <details>
            <summary><a href={linkArticle} target="_blank"><b>{title}</b></a><br> {pubDate}</summary>
            <p>{@html description}</p>
        </details>
        
        
    </div>
</main>

<style>
	.box {
        margin-top: 25px; 
    }
</style>