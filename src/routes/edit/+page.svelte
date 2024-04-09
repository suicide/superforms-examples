<script lang="ts">
	import { page } from '$app/stores';
	import { superForm, defaults, message } from 'sveltekit-superforms';
	import SuperDebug from 'sveltekit-superforms';
  import { zod } from 'sveltekit-superforms/adapters';
  import {schema} from '../schema';

	export let data;

  const form = superForm(
    defaults(zod(schema)),
    {
      SPA: true,
      dataType: 'json',
      validators: zod(schema),
      onUpdate: async ({ form }) => {
        console.log('hello world', form);
        message(form, 'Form posted successfully!');
        return true;
      }
    }
  );

  const { form: formData, message: msg, errors, enhance } = form;
</script>

<SuperDebug data={$formData} />

<h3>EDIT PAGE</h3>

{#if $msg}
	<!-- eslint-disable-next-line svelte/valid-compile -->
	<div class="status" class:error={$page.status >= 400} class:success={$page.status == 200}>
		{$msg}
	</div>
{/if}

<form method="POST" use:enhance>
	<label>
		Name<br />
		<input name="name" aria-invalid={$errors.name ? 'true' : undefined} bind:value={$formData.name} />
		{#if $errors.name}<span class="invalid">{$errors.name}</span>{/if}
	</label>

	<label>
		Email<br />
		<input
			name="email"
			type="email"
			aria-invalid={$errors.email ? 'true' : undefined}
			bind:value={$formData.email}
		/>
		{#if $errors.email}<span class="invalid">{$errors.email}</span>{/if}
	</label>

	<button>Submit</button>
</form>

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

