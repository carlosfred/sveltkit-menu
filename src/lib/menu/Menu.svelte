<script>
	import { slide } from 'svelte/transition';
	import FaAngleDown from 'svelte-icons/fa/FaAngleDown.svelte';
	import FaAngleRight from 'svelte-icons/fa/FaAngleRight.svelte';

	import menuItens from './menu.json';

	let dataMenu = menuItens;

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
	.container {
		margin: 0;
		width: 100%;
		min-height: 100vh;
		background-color: #2f4050;
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
		font-weight: bold;
		background-color: #253746;
	}

	.item a {
		color: #a7b1c2;
		text-decoration: none;
	}

	.item a:hover {
		color: #fff;
	}
</style>