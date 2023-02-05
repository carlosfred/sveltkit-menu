<script>
	import Menu from '$lib/menu/Menu.svelte';
</script>

<div class='container'>
	<div class='menu'><Menu /></div>
	<div class='content'><slot /></div>
</div>

<style>

	:global(*) {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	.container {
		display: flex;
		margin: 0;
		padding: 0;
	}

	.menu {
		width: 220px;
		min-height: 100vh;
		background-color: darkslateblue;
	}

	.content {
		flex: 1;
		min-height: 100vh;
		background-color: aquamarine;
	}
	
</style>