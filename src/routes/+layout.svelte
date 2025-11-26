<script>
	import favicon from '$lib/assets/favicon.svg';
	import Good from '$lib/assets/Good.png'
    
	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

{@render children()}
