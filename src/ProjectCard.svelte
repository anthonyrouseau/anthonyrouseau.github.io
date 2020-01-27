<script>
    export let name = "Name";
    export let description = "description";
    export let link = "https://github.com/anthonyrouseau";
</script>

<style>
    div{
        box-sizing: border-box;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        align-items: center;
        width: 75%;
        padding: 1% 1%;
        border: 2px solid var(--primary-dark);
        border-radius: 0.5em;
        box-shadow: 1px 2px 5px 2px #a9a9a9;
        overflow-y: scroll;
        -ms-overflow-style: none;
    }
    div::-webkit-scrollbar{
		display: none;
	}
    p{
        text-align: center;
        font-size: 3vw;
    }
    h1{
        font-size: 3vw;
        padding: 0;
    }
    a {
        color: var(--primary-dark);
        text-decoration: none;
        font-weight: bold;
    }
    a:hover {
        color: var(--secondary);
        cursor: pointer;
    }
    @media only screen and (min-width: 1200px) {
        div{
            border: none;
            box-shadow: none;
        }
    }
</style>

<div id="project-card">
    <h1>{name}</h1>
    <p>
       {description}
    </p>
    <a href={link}>Source Code</a>
</div>