<script>
    export let school;
    export let degree;
</script>

<style>
    div {
        display: flex;
        box-sizing: border-box;
        height: 100%;
        width: 80%;
        flex-direction: column;
        align-content: center;
        justify-content: center;
        align-self: center;
        border: 2px solid var(--primary-dark);
        border-radius: 0.5em;
        padding: 1%;
        box-shadow: 1px 2px 5px 2px #a9a9a9;
    }
    h2 {
        box-sizing: border-box;
        text-align: center;
        width: 15vw;
        align-self: center;
        padding: 5px;
        margin: 0;
        color: black;
        border-bottom: 2px solid var(--primary-dark);
    }
    ul {
        list-style: none;
        padding: 0;
	}
	li {
		margin-bottom: 10px;
    }
    @media only screen and (min-width: 1200px) {
        div{
            border: none;
            box-shadow: none;
            padding: 1% 0;
            width: 100%;
            justify-content: flex-start;
        }
    }
</style>

<div>
    <h2>Education</h2>
    <ul>
        <li>{school}</li>
        <li>{degree}</li>
    </ul>
</div>
