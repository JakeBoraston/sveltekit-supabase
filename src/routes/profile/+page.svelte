<script lang="ts">

	import UpdateProfile from '$lib/components/UpdateProfile.svelte';
	
	export let data;
	let avatar: string;

	// Reactive statement to update avatar when data changes
	$: userProfile = data.session?.user || '';
	$: avatar = data?.session?.user?.user_metadata?.avatar_url || '';
</script>

{#if userProfile}
	<UpdateProfile {userProfile} {avatar} />
{:else}

{/if}
