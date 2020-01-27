<script>
	export let phone;
	export let email;
</script>

<style>
	div {
		box-sizing: border-box;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-content: center;
		text-align: center;
		height: 100%;
		width: 90%;
		background-color: rgba(0, 0, 0, 0.3);
		border-radius: 1em;
		color: white;
		align-self: center;
    }
    h1,h2 {
			margin: 5px 0;
	}
	@media only screen and (min-width: 1200px) {
        div{
            border: none;
			box-shadow: none;
			background-color: transparent;
			color: black;
			width: 100%;
        }
    }
</style>


<div>
    <h1 class="headline">Anthony Rouseau</h1>
    <h2 class="sub-headline">Full Stack Developer</h2>
    <span>Phone: {phone}</span>
    <span>Email: {email}</span>
</div>