<script>
  let members = [];
  let newMember = '';

  function addMember() {
	members = [...members, { name: newMember }];
	newMember = '';
  }

  function deleteMember(index) {
	members = members.filter((_, i) => i !== index);
  }
</script>

<h1>Members</h1>
<input bind:value={newMember} placeholder="New Member"/>
<button on:click={addMember}>Add Member</button>

<ul>
  {#each members as member, index}
	<li>
	  {member.name}
	  <button on:click={() => deleteMember(index)}>Delete</button>
	</li>
  {/each}
</ul>