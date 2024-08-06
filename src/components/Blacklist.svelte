<script>
  let blacklist = [];
  let newEntry = '';

  function addEntry() {
	blacklist = [...blacklist, { name: newEntry }];
	newEntry = '';
  }

  function deleteEntry(index) {
	blacklist = blacklist.filter((_, i) => i !== index);
  }
</script>

<h1>Blacklist</h1>
<input bind:value={newEntry} placeholder="New Entry"/>
<button on:click={addEntry}>Add Entry</button>

<ul>
  {#each blacklist as entry, index}
	<li>
	  {entry.name}
	  <button on:click={() => deleteEntry(index)}>Delete</button>
	</li>
  {/each}
</ul>