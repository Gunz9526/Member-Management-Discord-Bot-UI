<script>
    import { onMount } from 'svelte';
    import { replace } from 'svelte-spa-router';
   
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
          body: JSON.stringify({ "session_name":params.session_name })
        });
        const data = await response.json();
        token = data.token;
        console.log('Token:', token, 'session_id:', data.session_id);
      } catch (error) {
        console.error('Error fetching token:', error);
      }
    }
  
    function handleOk() {
      replace('/dashboard');
    }
  </script>
  
  <h1>Authentication</h1>
  <p>Session: {params.session_name}</p>
  <p>Token: {token}</p>
  <button on:click={handleOk}>OK</button>
  

   <!-- src/components/Session.svelte -->
<!-- <script>
  export let session_name;
</script>

<h1>Session Page</h1>
<p>Session Name: {session_name}</p> -->
