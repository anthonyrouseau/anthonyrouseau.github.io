<script>
    export let items;

    let current = 0;


    function goForward() {
        document.getElementById("project-card").scrollTop = 0;
        current += 1;
        if(current >= items.length){
            current = 0;
        }
    }
    function goBack() {
        document.getElementById("project-card").scrollTop = 0;
        current -= 1;
        if(current < 0){
            current = (items.length - 1);
        }
    }
</script>

<style>
    div{
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        box-sizing: border-box;
        width: 100%;
        flex-grow: 1;
        overflow-y: scroll;
    }
    span{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100%;
        width: 6.25%;
        text-decoration: none;
        font-size: 5vw;
        color: var(--primary);
        align-self: center;
        border-radius: 0.25em;
    }
    span:hover{
        color: var(--secondary);
        cursor: pointer;
    }
</style>

<div id="project-carousel">
    <span on:click={goBack}>&#8249;</span>
    <slot  active={items[current]}></slot>
    <span on:click={goForward}>&#8250;</span>
</div>