<script lang="ts">
	// TODO: after mouseleave tooltip, it shouldn't appear
	// tried hidden, invisible but they don't work with opacity transition

	import classNames from 'classnames';
	import { clickOutside } from '$lib/utils/clickOutside';

	import {
		computePosition,
		flip,
		shift,
		offset,
		autoPlacement,
		arrow as arrowFloat,
		type ComputePositionReturn
	} from '@floating-ui/dom';
	import type { Placement } from '@floating-ui/dom';
	import { onDestroy } from 'svelte';

	export let placement: 'auto' | Placement = 'top';
	export let trigger: 'hover' | 'click' = 'hover';
	export let style: 'dark' | 'light' | 'auto' | 'custom' = 'dark';
	export let animation: false | `duration-${number}` = 'duration-500';
	export let arrow: boolean = true;
	export let popOverClass: string =
		'absolute inline-block z-10 text-gray-500 bg-white rounded-lg border border-gray-200 shadow-sm dark:text-gray-400 dark:border-gray-600 dark:bg-gray-800';
	export let tipColor: string = '';
	// let invisible = false;

	const tipStyleClasses = {
		dark: 'bg-gray-900 text-white dark:bg-gray-700',
		light: 'border border-gray-200 bg-white text-gray-900',
		auto: 'border border-gray-200 bg-white text-gray-900 dark:border-none dark:bg-gray-700 dark:text-white',
		custom: tipColor
	};

	const arrowStyleClasses = {
		dark: 'bg-gray-900 dark:bg-gray-700',
		light: 'bg-white',
		auto: 'bg-white dark:bg-gray-700',
		custom: tipColor
	};

	let toolTipClass;
	$: toolTipClass = classNames(
		popOverClass,
		animation !== false && `transition-opacity ${animation}`,
		// animation !== false && open && `transition-opacity ${animation} opacity-100`,
		!open && 'opacity-0',
		// invisible && 'invisible',
		tipStyleClasses[style],
		$$props.class
	);
	let open = false;
	const floatingPlacement = (placement: 'auto' | Placement): Placement | undefined => {
		return placement === 'auto' ? undefined : placement;
	};

	const floatingMiddleware = (arrowRef: any, placement: 'auto' | Placement) => {
		const middleware = [];
		middleware.push(offset(8));
		middleware.push(placement === 'auto' ? autoPlacement() : flip());
		middleware.push(shift({ padding: 8 }));
		if (arrowRef) {
			middleware.push(arrowFloat({ element: arrowRef }));
		}
		return middleware;
	};
	let placementData: ComputePositionReturn;
	let tooltipRef: HTMLElement, triggerRef: HTMLElement, arrowRef: HTMLElement;
	const updatePosition = () =>
		computePosition(triggerRef as Element, tooltipRef as HTMLElement, {
			middleware: floatingMiddleware(arrowRef, placement),
			placement: floatingPlacement(placement)
		}).then((data) => (placementData = data));
	let attachedScroll: boolean = false;
	$: tooltipRef && open && updatePosition();
	$: {
		if (open && !attachedScroll) {
			attachedScroll = true;
			window.addEventListener('scroll', updatePosition, true);
		} else if (!open && attachedScroll) {
			attachedScroll = false;
			window.removeEventListener('scroll', updatePosition, true);
		}
	}
	onDestroy(() => {
		if (attachedScroll) {
			attachedScroll = false;
			window.removeEventListener('scroll', updatePosition, true);
		}
	});

	const arrPos = {
		top: 'bottom',
		right: 'left',
		bottom: 'top',
		left: 'right'
	};

	let floatingArrowPlacement;
	$: {
		if (placementData) {
			const arrow = placementData.middlewareData.arrow;
			const pos = arrPos[placementData?.placement?.split('-')[0]] ?? 'top';
			if (pos === 'top' || pos === 'bottom')
				floatingArrowPlacement = `${pos}: -4px; left: ${px(arrow?.x)}`;
			else floatingArrowPlacement = `${pos}: -4px; top: ${px(arrow?.y)}`;
		}
	}

	const px = (x) => (x === undefined ? '' : x + 'px');
</script>

<svelte:window on:resize={() => open && updatePosition()} />

<div
	use:clickOutside={() => {
		if (open) {
			open = false;
			// invisible = false;
		}
	}}
	on:mouseleave={() => {
		if (open && trigger === 'hover') {
			open = false;
			// invisible = true;
		}
	}}
	on:mouseenter={() => {
		if (trigger === 'hover') {
			open = true;
			// invisible = false;
		}
	}}
>
	<div
		bind:this={triggerRef}
		class="w-fit"
		on:click={() => {
			if (trigger === 'click') {
				open = !open;
			}
		}}
	>
		<slot />
	</div>

	<div
		bind:this={tooltipRef}
		data-testid="tooltip"
		class={toolTipClass}
		style:left={px(placementData?.x)}
		style:top={px(placementData?.y)}
		style:position={placementData?.strategy ?? ''}
	>
		<slot name="content" />

		{#if arrow}
			<div
				class={classNames('absolute z-10 h-2 w-2 rotate-45', arrowStyleClasses[style])}
				data-testid="tooltip-arrow"
				style={floatingArrowPlacement}
				bind:this={arrowRef}
			>
				&nbsp;
			</div>
		{/if}
	</div>
</div>
