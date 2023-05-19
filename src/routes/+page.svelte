<script lang="ts">
	import { enhance, type SubmitFunction } from '$app/forms';
	import { createSupabaseLoadClient } from '@supabase/auth-helpers-sveltekit';
	import type { PageData } from './$types';
	export let data: PageData;
	import type { Database } from '$lib/DatabaseDefinitions';
	import { PUBLIC_SUPABASE_ANON_KEY, PUBLIC_SUPABASE_URL } from '$env/static/public';

	const submitLogout: SubmitFunction = async ({ cancel }) => {
		const { error } = await createSupabaseLoadClient<Database>({
			supabaseUrl: PUBLIC_SUPABASE_URL,
			supabaseKey: PUBLIC_SUPABASE_ANON_KEY,
			event: { fetch },
			serverSession: data.session
		}).auth.signOut();
		if (error) {
			console.log(error)
		}
		cancel();
	};
</script>

<main class="container">
	<article>
		<header>
			<h1>SvelteKit & Supabase Auth</h1>
		</header>
		{#if data.session}
			<p>Welcome, {data.session.user.email}</p>
			<form action="/logout" method="post" use:enhance={submitLogout}>
				<button type="submit"> Logout </button>
			</form>
		{:else}
			<p>Let's learn how to register and login users!</p>
			<div class="grid">
				<a href="/login" role="button">Login</a>
				<a href="/register" role="button" class="secondary">Register</a>
			</div>
		{/if}
	</article>
</main>
