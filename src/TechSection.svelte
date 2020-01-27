<script>
    export let list;
</script>

<style>
    h2 {
        box-sizing: border-box;
        text-align: center;
        width: 20vw;
        align-self: center;
        padding: 5px;
        margin: 0;
        margin-bottom: 1%;
        color: black;
        border-bottom: 2px solid var(--primary-dark);
    }
    .icon-container {
		display: flex;
		flex-direction: row;
		height: 100%;
		width: 100%;
		flex-wrap: wrap;
		justify-content: space-evenly;
		overflow-y: scroll;
    }
    figure {
		display: flex;
		flex-direction: column;
        align-content: center;
    }
    img {
        height: 10vh;
        width: auto;
    }
    figcaption{
        margin-top: 2px;
    }
    @media only screen and (min-width: 1200px) {
        img {
            height: 16vh;
            width: auto;
        }
    }
</style>

<h2>Tech Skills</h2>
<div class="icon-container">
    {#each list as item }
        <figure>
            <img src={item.imageUrl} alt={`${item.text} icon`}>
            <figcaption>{item.text}</figcaption>
        </figure>
    {/each}
</div>