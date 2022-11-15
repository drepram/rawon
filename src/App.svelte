<!-- https://github.com/sveltejs/svelte-virtual-list -->

<script>
	import VirtualList from './VirtualList.svelte';
	import items from './data.js';
	import ListItem from './ListItem.svelte';

	let searchTerm = "";
	
	// $: filteredList = items.filter(item => item.name.indexOf(searchTerm) !== -1);
	$: filteredList = items.filter(item => {
		const arr = searchTerm.split(' ').filter((character) => character != ''); // Filter to remove spaces (it will match any name that has space in it)
		return arr.some(el => item.nama.toLowerCase().includes(el) || item.npm.toLowerCase().includes(el) || item.jurusan.toLowerCase().includes(el) || item.fakultas.toLowerCase().includes(el));
		// The filtering is a work in progress. For now, one defect can be found with the string: `Andre Christoga`
		// Just the string `andre` would give 6 results. But when the string is `andre christ`, the results increases; shouldn't it decreases instead?
  })
	
  let start;
  let end;
	
</script>

<h1>Rawon</h1>
<p>Samudra profil mahasiswa UI! Data saat ini baru dari FMIPA saja.</p>
<p>Situs ini diprakarsai <a href="https://drepram.com">drepram</a> (FMIPA '20). </p>

Masukkan nama/npm/jurusan/fakultas: <input bind:value={searchTerm} />

<div class='container'>
	<VirtualList items={filteredList} bind:start bind:end let:item>
		<ListItem {...item}/>
	</VirtualList>
	<p>showing items {start}-{end}</p>
</div>

<style>
	.container {
		border-top: 1px solid #333;
		border-bottom: 1px solid #333;
		min-height: 200px;
		height: calc(100vh - 15em);
	}
</style>