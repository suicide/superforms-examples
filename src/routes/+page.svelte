<script lang="ts">
	import { page } from '$app/stores';
  import { pushState } from '$app/navigation';
	import SuperDebug from 'sveltekit-superforms';

  import EditPage from './edit/+page.svelte';


  const openEdit = () => pushState('/edit', {shallowEdit: true});
</script>


<h3>HOME PAGE</h3>
<button on:click={openEdit}>shallow edit</button>

{#if $page.state.shallowEdit}
  <EditPage />
{/if}
<SuperDebug label="$page data" data={$page} collapsible />


<hr />
<p>
	💥 <a target="_blank" href="https://superforms.rocks">Created with Superforms for SvelteKit</a> 💥
</p>

<style>
	.invalid {
		color: red;
	}

	.status {
		color: white;
		padding: 4px;
		padding-left: 8px;
		border-radius: 2px;
		font-weight: 500;
	}

	.status.success {
		background-color: seagreen;
	}

	.status.error {
		background-color: #ff2a02;
	}

	input {
		background-color: #ddd;
	}

	a {
		text-decoration: underline;
	}

	hr {
		margin-top: 4rem;
	}

	form {
		padding-top: 1rem;
		padding-bottom: 1rem;
	}
</style>
