<!-- https://github.com/sveltejs/svelte-virtual-list -->

<script>
	import VirtualList from './VirtualList.svelte';
	import items from './data.js';
	import ListItem from './ListItem.svelte';

	let searchTerm = "";
	
	$: filteredList = searchTerm ? items.filter(item => {
		const query = searchTerm.toLowerCase()
		return item.nama.toLowerCase().includes(query) || item.npm.toLowerCase().includes(query) || item.jurusan.toLowerCase().includes(query) || item.fakultas.toLowerCase().includes(query)
	}) : [];
	
  let start;
  let end;
	
</script>

<h1>Rawon</h1>
<p>Samudra profil mahasiswa UI! Data saat ini baru dari FMIPA saja.</p>
<p>Situs ini diprakarsai <a href="https://instagram.com/drepram">drepram</a> (FMIPA '20).</p>

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
