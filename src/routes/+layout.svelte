<script>
	import '../app.css';
	import { goto, invalidate } from '$app/navigation';
	import { ModeWatcher } from 'mode-watcher';
	import { Button } from '$lib/components/ui/button';
	import * as Avatar from '$lib/components/ui/avatar';

	const { data: propsData, children } = $props();

	const { supabase, session } = propsData;

	$effect(() => {
		const { data } = supabase.auth.onAuthStateChange((_, newSession) => {
			if (!newSession) {
				/**
				 * Queue this as a task so the navigation won't prevent the
				 * triggering function from completing
				 */
				setTimeout(() => {
					goto('/', { invalidateAll: true });
				});
			}
			if (newSession?.expires_at !== session?.expires_at) {
				invalidate('supabase:auth');
			}
		});

		return () => data.subscription.unsubscribe();
	});
</script>

<ModeWatcher />

<div class="flex min-h-screen flex-col">
	<nav class="p-4">
		<div class="mx-auto flex flex w-full max-w-2xl justify-between">
			{#if session !== null}
				<a href="/" class="text-2xl font-black">Strength App</a>
				<a href="/profile">
					<Avatar.Root>
						<Avatar.Image src={session.user.user_metadata.avatar_url} alt="Profile picture" />
						<Avatar.Fallback>{session.user.user_metadata.user_name[0]}</Avatar.Fallback>
					</Avatar.Root>
				</a>
			{/if}
		</div>
	</nav>

	<main class="mx-auto w-full max-w-2xl flex-grow px-2 py-5 md:px-0">
		{@render children()}
	</main>
</div>

<style>
	html,
	body {
		height: 100%;
		margin: 0;
		padding: 0;
	}
	* {
		font-family: 'Inter', sans-serif;
	}
</style>
