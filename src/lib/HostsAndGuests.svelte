<script lang="ts">
	import type { Guest } from '@prisma/client';
	import Host from '$lib/hosts/Host.svelte';
	export let guests: { Guest: Guest }[] = [];
	export let hosts: {
		name: string | null;
		username: string | null;
		twitter: string | null;
	}[] = [];
</script>

<div class="guests-and-hosts">
	{#if guests?.length > 0}
		{#each guests as { Guest }}
			<Host
				host={{
					name: Guest.name,
					github: Guest?.github,
					twitter: Guest?.twitter,
					slug: Guest?.name_slug
				}}
				guest={true}
			/>
		{/each}
	{/if}
	{#if hosts.length > 0}
		{#each hosts as host}
			<Host
				host={{
					name: host.name || '',
					github: host.username,
					twitter: host.twitter
				}}
			/>
		{/each}
	{:else}
		<Host
			host={{
				name: 'Wes Bos',
				github: 'wesbos',
				twitter: 'wesbos'
			}}
		/>
		<Host
			host={{
				name: 'Scott Tolinski',
				github: 'stolinski',
				twitter: 'stolinski'
			}}
		/>
	{/if}
</div>

<style lang="postcss">
	.guests-and-hosts {
		margin: 2rem 0;
		display: flex;
		gap: 1rem;
		flex-wrap: wrap;
	}
</style>
