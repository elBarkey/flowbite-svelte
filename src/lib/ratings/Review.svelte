<script lang="ts">
	import type { ReviewType } from '$lib/types';
	import classNames from 'classnames';
	export let review: ReviewType;
	export let articleClass: string = 'md:gap-8 md:grid md:grid-cols-3';
	export let divClass: string = 'flex items-center mb-6 space-x-4';
	export let imgClass: string = 'w-10 h-10 rounded-full';
	export let ulClass: string = 'space-y-4 text-sm text-gray-500 dark:text-gray-400';
	export let liClass: string = 'flex items-center';
</script>

<article class={classNames(articleClass, $$props.classArticle)}>
	<div>
		<div class={classNames(divClass, $$props.classDiv)}>
			<img class={classNames(imgClass, $$props.classImg)} src={review.imgSrc} alt={review.imgAlt} />
			<div class="space-y-1 font-medium dark:text-white">
				<p>{review.name}</p>
				{#if review.address}
					<div class="flex items-center text-sm text-gray-500 dark:text-gray-400">
						{#if review.addressIcon}
							<svelte:component this={review.addressIcon} size="16" class="mr-2" />
						{/if}
						{review.address}
					</div>
				{/if}
			</div>
		</div>
		{#if $$slots.item || $$slots.option1 || $$slots.option2}
			<ul class={classNames(ulClass, $$props.classUl)}>
				{#if $$slots.item}
					<li class={classNames(liClass, $$props.classLi)}>
						<slot name="item" />
					</li>
				{/if}
				{#if $$slots.option1}
					<li class={classNames(liClass, $$props.classLi)}>
						<slot name="option1" />
					</li>
				{/if}
				{#if $$slots.option2}
					<li class={classNames(liClass, $$props.classLi)}>
						<slot name="option2" />
					</li>
				{/if}
			</ul>
		{/if}
	</div>
	<div class="col-span-2 mt-6 md:mt-0">
		<div class="flex items-start mb-5">
			<div class="pr-4">
				{#if review.reviewDate}
					<footer>
						<p class="mb-2 text-sm text-gray-500 dark:text-gray-400">
							Reviewed: {review.reviewDate}
						</p>
					</footer>
				{/if}
				<h4 class="text-xl font-bold text-gray-900 dark:text-white">
					{review.title}
				</h4>
			</div>
			<p
				class="bg-blue-700 text-white text-sm font-semibold inline-flex items-center p-1.5 rounded"
			>
				{review.rating}
			</p>
		</div>
		<slot />
	</div>
</article>
