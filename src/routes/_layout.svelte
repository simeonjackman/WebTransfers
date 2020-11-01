<script>
	import Nav from '../components/Nav.svelte';

	export let segment;
</script>

<style global>
	@tailwind base;
	@tailwind components;
	@tailwind utilities;
</style>

<Nav {segment}/>

<main>
<div class="container mx-auto p-4">
	<slot></slot>
</div>
</main>