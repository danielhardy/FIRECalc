<script lang="ts">
	import '../app.css';
	import {page} from '$app/stores';

	//Put nav here;
	const nav =[
	]

	const userMenu = ()=>{
		console.log("You should figure out how to make this work")
	}
</script>

<nav class="navbar bg-base-100 px-4 py-0 mb-8">
	<div class="flex-none">
		<h1 class="logo text-lg font-bold">🔥 Calculator</h1>
	</div>
	<div class="flex-1 mx-12">
		<ul class="menu horizontal">
			{#each nav as item}
				<li class:bordered={$page.path === item.path}><a href="{item.path}" class="">{item.title}</a></li>
			{/each}
		</ul>
	</div>
	<div class="flex-none">
	</div>
</nav>

<slot />
