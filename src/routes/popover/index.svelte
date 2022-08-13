<script lang="ts">
	import {
		Htwo,
		ExampleDiv,
		GitHubSource,
		CompoDescription,
		TableProp,
		TableDefaultRow
	} from '../utils';
	import { Popover, Button, Avatar } from '$lib';
	import { GlobeAlt, Heart, DotsHorizontal } from 'svelte-heros';
</script>

<ExampleDiv class="h-64 flex items-end justify-center">
	<Popover
		isPopover
		style="custom"
		tipColor="bg-white dark:bg-gray-800 border-r border-b border-gray-200 dark:border-gray-600"
		class="w-64"
	>
		<Button>Default popover</Button>
		<svelte:fragment slot="content">
			<div
				class="py-2 px-3 bg-gray-100 rounded-t-lg border-b border-gray-200 dark:border-gray-600 dark:bg-gray-700"
			>
				<h3 class="font-semibold text-gray-900 dark:text-white">Popover title</h3>
			</div>
			<div class="py-2 px-3">
				<p>And here's some amazing content. It's very engaging. Right?</p>
			</div>
		</svelte:fragment>
	</Popover>
</ExampleDiv>

<ExampleDiv class="h-80 flex items-end justify-center">
	<Popover
		isPopover
		style="custom"
		tipColor="bg-white dark:bg-gray-800 border-r border-b border-gray-200 dark:border-gray-600 "
	>
		<Button>User profile</Button>
		<svelte:fragment slot="content">
			<div class="p-3">
				<div class="flex justify-between items-center mb-2">
					<a href="/">
						<img
							class="w-10 h-10 rounded-full"
							src="/images/profile-picture-1.webp"
							alt="Jese Leos"
						/>
					</a>
					<div>
						<Button size="xs">Follow</Button>
					</div>
				</div>
				<p class="text-base font-semibold leading-none text-gray-900 dark:text-white">
					<a href="/">Jese Leos</a>
				</p>
				<p class="mb-3 text-sm font-normal">
					<a href="/" class="hover:underline">@jeseleos</a>
				</p>
				<p class="mb-4 text-sm font-light">
					Open-source contributor. Building <a
						href="/"
						class="text-blue-600 dark:text-blue-500 hover:underline">flowbite.com</a
					>.
				</p>
				<ul class="flex text-sm font-light">
					<li class="mr-2">
						<a href="/" class="hover:underline">
							<span class="font-semibold text-gray-900 dark:text-white">799</span>
							<span>Following</span>
						</a>
					</li>
					<li>
						<a href="/" class="hover:underline">
							<span class="font-semibold text-gray-900 dark:text-white">3,758</span>
							<span>Followers</span>
						</a>
					</li>
				</ul>
			</div>
		</svelte:fragment>
	</Popover>
</ExampleDiv>

<ExampleDiv
	divClass="h-96 pb-4 pt-8 flex items-end justify-center rounded-xl w-full my-4 mx-auto bg-gradient-to-r bg-white dark:bg-gray-900 border border-gray-200 dark:border-gray-700"
>
	<Popover
		isPopover
		style="custom"
		tipColor="bg-white dark:bg-gray-800 border-r border-b border-gray-200 dark:border-gray-600 "
		class="w-80"
	>
		<Button>Company profile</Button>
		<svelte:fragment slot="content">
			<div class="p-3">
				<div class="flex">
					<div class="mr-3 shrink-0">
						<a href="/" class="block p-2 bg-gray-100 rounded-lg dark:bg-gray-700">
							<img
								class="w-8 h-8 rounded-full"
								src="https://flowbite.com/docs/images/logo.svg"
								alt="Flowbite logo"
							/>
						</a>
					</div>
					<div>
						<p class="mb-1 text-base font-semibold leading-none text-gray-900 dark:text-white">
							<a href="/" class="hover:underline">Flowbite</a>
						</p>
						<p class="mb-3 text-sm font-normal">Tech company</p>
						<p class="mb-4 text-sm font-light">
							Open-source library of Tailwind CSS components and Figma design system.
						</p>
						<ul class="text-sm font-light">
							<li class="flex items-center mb-2">
								<span class="mr-1 font-semibold text-gray-400">
									<GlobeAlt size="16" />
								</span>
								<a href="/" class="text-blue-600 dark:text-blue-500 hover:underline"
									>https://flowbite.com/</a
								>
							</li>
							<li class="flex items-start mb-2">
								<span class="mr-1 font-semibold text-gray-400">
									<Heart size="16" variation="solid" />
								</span>
								<span>4,567,346 people like this including 5 of your friends</span>
							</li>
						</ul>
						<div class="flex mb-3 -space-x-3">
							<Avatar src="/images/profile-picture-1.webp" stacked />
							<Avatar src="/images/profile-picture-2.webp" stacked />
							<Avatar src="/images/profile-picture-3.webp" stacked />
							<Avatar
								stacked
								href="/"
								class="bg-gray-700 dark:bg-gray-700 text-white hover:bg-gray-600">+3</Avatar
							>
						</div>
						<div class="flex">
							<Button type="button" color="light" class="mr-2 w-full">
								<Heart size="14" variation="solid" class="mr-2" />
								Like page
							</Button>
							<button
								class="inline-flex items-center py-2 px-2 text-sm font-medium text-gray-900 bg-white rounded-lg border border-gray-200 shrink-0 focus:outline-none hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-4 focus:ring-gray-200 dark:focus:ring-gray-700 dark:bg-gray-800 dark:text-gray-400 dark:border-gray-600 dark:hover:text-white dark:hover:bg-gray-700"
								type="button"
							>
								<DotsHorizontal class="w-5 h-5" />
							</button>
						</div>
					</div>
				</div>
			</div></svelte:fragment
		>
	</Popover>
</ExampleDiv>
