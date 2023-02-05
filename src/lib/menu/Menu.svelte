<script>
	import { slide } from 'svelte/transition';
	import FaAngleDown from 'svelte-icons/fa/FaAngleDown.svelte';
	import FaAngleRight from 'svelte-icons/fa/FaAngleRight.svelte';

	import menuItens from './menu.json';

	let logo = menuItens.logo;
	let dataMenu = menuItens.grupos;

	const selecionaItem = (grupoId, itemId ) => {
		dataMenu.map((grupo) => {
			grupo.selecionado = grupo.id === grupoId;
			grupo.itens.map((item) => {
				item.selecionado = item.id === itemId && grupo.id === grupoId;
			})
		}) 
		dataMenu = dataMenu;
	};

	const toogleColapsed = (e) => {
		dataMenu[e].isCollapsed = !dataMenu[e].isCollapsed;
	};

</script>

<div class='container'>
	<div class="logo">
		<a href="/"><img src={logo} alt='' /></a>
	</div>
	{#each dataMenu as grupo}
		<div class="grupo {grupo.selecionado ? 'selecionado' : ''}">
			<div class='itemGrupo'>
				<div class='label'>{grupo.label}</div>
				<div class='icon' on:click={() => toogleColapsed(grupo.id)} on:keypress={() => toogleColapsed(grupo.id)}>
					{#if !grupo.isCollapsed}
						<FaAngleDown />
					{:else}
						<FaAngleRight />
					{/if}
				</div>
			</div>
			{#each grupo.itens as item}
				{#if !grupo.isCollapsed}
					<div transition:slide class='item'>
						<a href="{item.link}" class="{item.selecionado ? 'itemSelecionado' : ''}" 
						on:click={() => selecionaItem(grupo.id, item.id)}>{item.label}</a>
					</div>
				{/if}
			{/each}
		</div>
	{/each}
	<svg class="itemSelecionado" />
</div>

<style>
	@font-face {
        font-family: 'Gelasio';
        font-style: normal;
        font-weight: 400;
        src: local('Gelasio Regular'), local('Gelasio-Regular'), url(https://fonts.gstatic.com/s/gelasio/v1/cIf9MaFfvUQxTTqS9C6hYQ.woff2) format('woff2');
        unicode-range: U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+2000-206F, U+2074, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
    }

	.container {
		margin: 0;
		width: 100%;
		min-height: 100vh;
		background-color: #2f4050;
		font-family: Gelasio
	}

	.grupo {
		border-left: 4px solid transparent;
		justify-content: space-between;
	}

	.grupo.selecionado {
		border-color: #19ca54;
	}

	.grupo .itemGrupo {
		display: flex;
	}

	.itemGrupo .label {
		padding: 10px 0 0 20px;
		color: #fff;
		flex: 1;
	}	

	.itemGrupo .icon {
		width: 20px;
		height: 20px;
		margin: 10px 5px 0 0;
		color: #fff;
		font-size: 10px;
		cursor: pointer;
	}

	svg {
		fill: currentColor;
	}

	.item {
		color: #a7b1c2;
		padding: 8px 0 8px 35px;
		cursor: pointer;
	}

	.item:hover {
		color: #fff;
		font-weight: 500;
		background-color: #253746;
	}

	.item a {
		display: block;
		width: 100%;
		color: #a7b1c2;
		text-decoration: none;
	}

	.item a:hover {
		color: #fff;
	}


</style>