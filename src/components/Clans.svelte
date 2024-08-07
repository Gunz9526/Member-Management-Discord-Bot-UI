<script>
  import { onMount } from 'svelte';
  import { validCheck } from '../util/validcheck';
  let clans = [];
  let newClan = '';
  let clan_list = [];

  onMount(() => {
    validCheck()
    all_clan()
  });

  async function all_clan() {
      try {
        const response = await fetch(`http://107.191.60.127:5000/member/all_clan`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
            'Authorization': 'Bearer ' + sessionStorage.getItem('token')
          },
          body: JSON.stringify({"session_id": sessionStorage.getItem('session_id'),"session_name": sessionStorage.getItem('session_name'), "tokens": sessionStorage.getItem('token')})
        });
        const data = await response.json();
        if (data.result == 'success') {
          console.log(data.clan_list)
          clan_list = data.clan_list
        }
        
      } catch (error) {
        console.error('Error fetching token:', error);
      }
    }


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
  {#each clan_list as clan, index}
	<li>
	  {clan[1]}
	  <button on:click={() => deleteClan(index)}>Delete</button>
	</li>
  {/each}
</ul>