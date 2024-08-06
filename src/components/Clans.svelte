<script>
  let clans = [];
  let newClan = '';

  function addClan() {
	clans = [...clans, { name: newClan }];
	newClan = '';
  }

  function deleteClan(index) {
	clans = clans.filter((_, i) => i !== index);
  }
</script>

<h1>Clans</h1>
<input bind:value={newClan} placeholder="New Clan"/>
<button on:click={addClan}>Add Clan</button>

<ul>
  {#each clans as clan, index}
	<li>
	  {clan.name}
	  <button on:click={() => deleteClan(index)}>Delete</button>
	</li>
  {/each}
</ul>