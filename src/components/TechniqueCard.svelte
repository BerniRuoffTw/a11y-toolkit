<script lang="ts">
	import type { Components, Level } from '$types/types';
	import Tag from './Tag.svelte';
	import { browser } from '$app/environment';
	import { onMount } from 'svelte';

	export let href: string;
	export let title: string;
	export let description: string;
	export let level: Level;
	export let components: Components[] = [];

	let slug = href.slice(1);

	let resolved: boolean = false;
	let resolvedList: string[];
	$: resolvedClass = resolved ? 'resolved' : '';

	onMount(() => {
		if (browser) {
			resolvedList = JSON.parse(localStorage.getItem('resolvedList') || '[]');
			if (resolvedList.includes(slug)) {
				resolved = true;
			} else {
				resolved = false;
			}
		}
	});
</script>

<div class="technique {resolvedClass}">
	{#if resolved}
		<div class="sr-only">Marked as resolved:</div>
	{/if}

	<a {href} class="technique-title">{title}</a>
	{#if description && !resolved}
		<p>{description || 'No description available.'}</p>
	{/if}
	{#if !resolved}
		<ul class="tag-list">
			{#if level}
				<li>
					<Tag value="WCAG 2.2" />
				</li>
				<li>
					<Tag value={level} />
				</li>
			{/if}

			{#if components.length > 0}
				{#each components as component}
					<li>
						<a href="/component/{component}" class="tag surface-link">&num;{component}</a>
					</li>
				{/each}
			{/if}
		</ul>
	{/if}
</div>

<style lang="scss">
	.technique {
		padding-block: var(--size-3);
		padding-inline: var(--size-4);
		border-color: var(--border);
		border-width: var(--border-size-1);
		border-radius: var(--radius-3);
		display: flex;
		flex-direction: column;
		gap: var(--size-1);

		a {
			text-decoration: none;
		}

		p {
			text-wrap: balance;
			font-size: var(--font-size-fluid-0);
			line-height: var(--font-lineheight-1);
			color: var(--text-2);
		}

		.technique-title {
			display: block;
			font-size: var(--font-size-fluid-1);
			line-height: var(--font-lineheight-1);
			text-wrap: balance;
			margin-bottom: var(--size-2);
		}

		&:hover {
			background-color: var(--surface-2);
			box-shadow: 0 0 0 2px var(--border);
		}

		&.resolved {
			opacity: 0.6;

			.technique-title {
				text-decoration: line-through;
				margin-bottom: 0;
			}
		}
	}

	.tag-list {
		list-style: none;
		display: flex;
		gap: var(--size-2);
		padding: 0;
		margin-top: var(--size-2);

		li {
			padding: 0;
		}
	}
</style>
