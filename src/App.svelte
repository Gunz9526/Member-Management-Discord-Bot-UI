<script>
	import Router from 'svelte-spa-router';
	import Session from "./components/Session.svelte";
	import Dashboard from "./components/Dashboard.svelte";
	import { onMount } from 'svelte';
	import { location, push } from 'svelte-spa-router';
 
	const routes = {
	  '/' : Session,
	  '/session/:session_name': Session,
	  '/dashboard': Dashboard,
	};

	// function updateTitle(route) {
    //     const routeName = route.split('/')[1];
    //     document.title = routeName ? `Current Page: ${routeName}` : 'ㅎㅇ';
    // }

    // // Svelte의 반응성 사용
    // $: updateTitle($location);

    onMount(() => {
		console.log('Current location:', $location);
		
		// push('/session/1234');
        // 페이지가 처음 로드될 때 제목을 설정
        // updateTitle($location);
    });
</script>

<Router {routes} />
