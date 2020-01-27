<script>
    export let text;
</script>

<style>
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
    div {
        box-sizing: border-box;
        display: flex;
        height: 100%;
        width: 80%;
        flex-direction: column;
        align-content: center;
        justify-content: center;
        align-self: center;
        border: 2px solid var(--primary-dark);
        border-radius: 0.5em;
        padding: 1% 10%;
        box-shadow: 1px 2px 5px 2px #a9a9a9;
    }
    p {
        margin: 5% 0;
    }
    @media only screen and (min-width: 1200px) {
        div{
            border: none;
            box-shadow: none;
            padding: 1% 0;
            width: 100%;
            border-radius: 1em;
            justify-content: flex-start;
        }
    }
</style>

<div>
    <h2>About Me</h2>
    <p>
        {text}
    </p>
</div>
