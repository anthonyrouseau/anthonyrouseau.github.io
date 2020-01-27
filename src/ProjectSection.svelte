<script>
    import Carousel from './Carousel.svelte';
    import ProjectCard from './ProjectCard.svelte';
    export let list;
</script>

<style>
    h2 {
        box-sizing: border-box;
        text-align: center;
        width: 15vw;
        align-self: center;
        padding: 5px;
        margin: 0;
        margin-bottom: 1%;
        color: black;
        border-bottom: 2px solid var(--primary-dark);
    }
    div{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100%;
        width: 100%;
    }
</style>

<div>
    <h2>Projects</h2>
    <Carousel items={list} let:active={project}>
        <ProjectCard {...project} />
    </Carousel>
</div>

