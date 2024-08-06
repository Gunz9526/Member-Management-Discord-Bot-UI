<script>
  import { writable } from 'svelte/store';
  import Clans from './Clans.svelte';
  import Members from './Members.svelte';
  import Blacklist from './Blacklist.svelte';

  let activeTab = writable('clans');
</script>

<style>
  .tabs {
	display: flex;
	cursor: pointer;
  }
  .tab {
	padding: 10px;
	border: 1px solid #ccc;
  }
  .active {
	background-color: #ddd;
  }
</style>

<div class="tabs">
    <div class="tab" class:active={$activeTab === 'clans'} on:click={() => activeTab.set('clans')}>Clans</div>
    <div class="tab" class:active={$activeTab === 'members'} on:click={() => activeTab.set('members')}>Members</div>
    <div class="tab" class:active={$activeTab === 'blacklist'} on:click={() => activeTab.set('blacklist')}>Blacklist</div>
</div>
  


{#if $activeTab === 'clans'}
  <Clans />
{:else if $activeTab === 'members'}
  <Members />
{:else if $activeTab === 'blacklist'}
  <Blacklist />
{/if}