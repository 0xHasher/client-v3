<script>
	import { _ } from '../../services/i18n';

	import Ticker from '../Ticker.svelte'
	import ChartResolution from '../ChartResolution.svelte'
	import Chart from '../Chart.svelte'
	import Order from '../Order.svelte'
	import Positions from '../Positions.svelte'
	import History from '../History.svelte'

	let panel = 'positions';

	function selectPanel(_panel) {
		panel = _panel;
	}

</script>

<style>

	.trade {
		display: grid;
		grid-gap: var(--grid-gap);
		grid-auto-flow: column;
		grid-template-columns: 300px auto;
		background-color: var(--rich-black-fogra);
		position: absolute;
		top: calc(var(--header-height) + var(--grid-gap));
		bottom: 0;
		left: 0;
		right: 0;
	}

	.sidebar {
		order: 1;
		background-color: var(--eerie-black);
	}

	.core {
		order: 2;
		display: grid;
		grid-gap: var(--grid-gap);
		grid-auto-flow: row;
		grid-template-rows: var(--ticker-height) var(--chart-resolution-height) var(--chart-height) auto;
	}

	.account {
		position: relative;
		background-color: var(--eerie-black);
	}

	.chart {

	}

	.account-nav {
		padding: 0 var(--base-padding);
		display: flex;
		height: 42px;
		align-items: center;
		border-bottom: 1px solid var(--jet-dim);
	}

	.account-list {
		position: absolute;
		top: 42px;
		bottom: 0;
		left: 0;
		right: 0;
		min-height: 100px;
		background-color: var(--eerie-black);
	}

	.account-nav a {
		color: var(--sonic-silver);
		margin-right: var(--base-padding);
	}
	.account-nav a:hover {
		color: var(--green);
	}
	.account-nav a.active {
		color: var(--green);
		font-weight: 600;
	}

	@media (max-width: 600px) {
		
		.trade {
			display: grid;
			grid-gap: var(--grid-gap);
			grid-auto-flow: row;
			grid-template-rows: auto;
			grid-template-columns: unset;
			overflow-y: scroll;
		}

		.core {
			order: 2;
		}

		.sidebar {
			order: 1;
		}

		.account-list {
			min-height: 300px;
		}

	}

</style>

<div class='trade no-scrollbar' id='trade'>

	<div class='core'>

		<Ticker />

		<ChartResolution />
		<Chart/>

		<div class='account'>

			<div class='account-nav'>
				<a class:active={panel == 'positions'} on:click={() => {selectPanel('positions')}}>{$_('comm.positions')}</a>
				<a class:active={panel == 'history'} on:click={() => {selectPanel('history')}}>{$_('comm.history')}</a>
			</div>

			<div class='account-list'>
				{#if panel == 'positions'}
					<Positions />
				{/if}
				{#if panel == 'history'}
					<History />
				{/if}
			</div>
		</div>

	</div>

	<div class='sidebar'>
		<Order />
	</div>

</div>