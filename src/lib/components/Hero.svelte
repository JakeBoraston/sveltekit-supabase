<script lang="ts">
	import { Button } from '$lib/components/ui/button';
	import * as Card from '$lib/components/ui/card/index';
	import Icon from '@iconify/svelte';
</script>

<div>
	<Card.Root class="mx-auto max-w-md">
		<Card.Header>
			<Card.Title class="text-3xl font-black">
				Sign in to Strength Tracker
			</Card.Title>

		</Card.Header>
		<Card.Content>
			<Button href="/auth/login" class="group/loginButton w-full">
				<div class="flex items-center gap-2">
					<div>Log in</div>
					<Icon
						icon="mdi:login"
						class="h-5 w-5 transition-all duration-300 md:group-hover/loginButton:translate-x-1"
					/>
				</div>
			</Button>
		</Card.Content>
	</Card.Root>
</div>
