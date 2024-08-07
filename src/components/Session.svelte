<script>
    import { onMount } from 'svelte';
    import { replace } from 'svelte-spa-router';
    let authorized = false;
    let token;
    export let params;
  
    onMount(() => {
      console.log('Sessi1on name:', params.session_name);
      fetchToken();
    });
    
    async function fetchToken() {
      try {
        const response = await fetch(`http://107.191.60.127:5000/session/get_token`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({"session_name":params.session_name})
        });
        const data = await response.json();
        if (data.result == 'success') {
          authorized = true;
          token = data.token;             
          sessionStorage.setItem('token', token );
          sessionStorage.setItem('session_id', data.session_id);
          sessionStorage.setItem('session_name', params.session_name);       
          console.log('Token:', token, 'session_id:', data.session_id);
          
        } else {
          console.error('Error fetching token:', data.error);
        }
        
      } catch (error) {
        console.error('Error fetching token:', error);
      }
    }

    async function session_expired() {
      try {
        await fetch(`http://107.191.60.127:5000/session/destroy_session`, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({ "session_name": sessionStorage.getItem('session_name') })
        });
        
      } catch (error) {
        console.error('Error fetching token:', error);
      }
    }
  
    function handleOk() {
      session_expired();
      replace('/dashboard');
    }
  </script>
  
  <h1>Authentication</h1>
  <p><b>State</b>: {#if authorized}Available{:else}Expired or Invalid{/if}</p>
  <p><b>Session</b>: {params.session_name}</p>
  <p><b>Token</b>: {token}</p>
  {#if authorized}
    <button on:click={handleOk}>OK</button>
  {/if}

   <!-- src/components/Session.svelte -->
<!-- <script>
  export let session_name;
</script>

<h1>Session Page</h1>
<p>Session Name: {session_name}</p> -->
