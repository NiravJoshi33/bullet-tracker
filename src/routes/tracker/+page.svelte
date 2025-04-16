<script lang="ts">
	import { AllCommunityModule, ModuleRegistry, type GridOptions } from 'ag-grid-community';
	import { createGrid } from 'ag-grid-community';
	import { activities } from '$lib/data';
	import { onMount } from 'svelte';

	import 'ag-grid-community/styles/ag-grid.css';
	import 'ag-grid-community/styles/ag-theme-quartz.css';

	ModuleRegistry.registerModules([AllCommunityModule]);

	const gridOptions: GridOptions = {
		rowData: activities,
		columnDefs: [
			{ headerName: 'Activity', field: 'name' },
			...Array.from({ length: 30 }, (_, i) => ({
				field: `${i + 1}`,
				editable: true,
				width: 42
			}))
		],
		maintainColumnOrder: true
	};

	onMount(() => {
		const gridElement = document.getElementById('grid-container');

		if (gridElement) {
			createGrid(gridElement, gridOptions);
		}
	});
</script>

<div>
	<h1>Tracker</h1>
	<div id="grid-container" class="ag-theme-quartz" style="width: 80%;"></div>
</div>

<style>
	#grid-container {
		height: 20rem;
	}
</style>
