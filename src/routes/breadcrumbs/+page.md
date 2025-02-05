---
layout: breadcrumbLayout
---

<script>
  import { Htwo, ExampleDiv, GitHubSource, CompoDescription, TableProp, TableDefaultRow} from '../utils'
  import { Breadcrumb, BreadcrumbItem } from '$lib'
  import { Home } from 'svelte-heros'
  
  import componentProps from '../props/Breadcrumb.json'
  import componentProps2 from '../props/BreadcrumbItem.json'
  let items = componentProps.props
  let items2 = componentProps2.props
  let propHeader = ['Name', 'Type', 'Default']
	let divClass='w-full relative overflow-x-auto shadow-md sm:rounded-lg py-4'
let theadClass ='text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-white'
</script>

<Breadcrumb>
  <BreadcrumbItem href="/" icon={Home} variation="solid">Home</BreadcrumbItem>
  <BreadcrumbItem>Breadcrumb</BreadcrumbItem>
</Breadcrumb>

<h1 class="text-3xl w-full dark:text-white pt-8 pb-4">Breadcrumb</h1>

<CompoDescription>Show the location of the current page in a hierarchical structure using the breadcrumb components</CompoDescription>

<ExampleDiv>
<GitHubSource href="breadcrumbs/Breadcrumb.svelte">Breadcrumb</GitHubSource>
<GitHubSource href="breadcrumbs/BreadcrumbItem.svelte">BreadcrumbItem</GitHubSource>
</ExampleDiv>

The breadcrumb component is an important part of any website or application that can be used to show the current location of a page in a hierarchical structure of pages.

Flowbite includes two styles of breadcrumb elements, one that has a transparent background and a few more that come with a background in different colors.

<Htwo label="Setup" />

```html
<script>
	import { Breadcrumb, BreadcrumbItem } from 'flowbite-svelte';
</script>
```

<Htwo label="Default Breadcrumb" />

Use the following breadcrumb example to show the hierarchical structure of pages.

<ExampleDiv>
<Breadcrumb aria-label="Default breadcrumb example">
  <BreadcrumbItem href="/" icon={Home} variation="solid">Home</BreadcrumbItem>
  <BreadcrumbItem href="/">Projects</BreadcrumbItem>
  <BreadcrumbItem>Flowbite Svelte</BreadcrumbItem>
</Breadcrumb>
</ExampleDiv>

```html
<Breadcrumb aria-label="Default breadcrumb example">
  <BreadcrumbItem href="/" icon={Home} variation="solid">Home</BreadcrumbItem>
  <BreadcrumbItem href="/">Projects</BreadcrumbItem>
  <BreadcrumbItem>Flowbite Svelte</BreadcrumbItem>
</Breadcrumb>
```

<Htwo label="Solid Breadcrumb" />

You can alternatively also use the breadcrumb components with a solid background.

<ExampleDiv>
<Breadcrumb aria-label="Solid background breadcrumb example" class="bg-gray-50 py-3 px-5 dark:bg-gray-900">
  <BreadcrumbItem href="/" icon={Home} variation="solid">Home</BreadcrumbItem>
  <BreadcrumbItem href="/">Projects</BreadcrumbItem>
  <BreadcrumbItem>Flowbite Svelte</BreadcrumbItem>
</Breadcrumb>
</ExampleDiv>

```html
<Breadcrumb aria-label="Solid background breadcrumb example" class="bg-gray-50 py-3 px-5 dark:bg-gray-900">
  <BreadcrumbItem href="/" icon={Home} variation="solid">Home</BreadcrumbItem>
  <BreadcrumbItem href="/">Projects</BreadcrumbItem>
  <BreadcrumbItem>Flowbite Svelte</BreadcrumbItem>
</Breadcrumb>
```

<Htwo label="Props" />

The component has the following props, type, and default values. See <a href="/pages/types">types page</a> for type information.

<h3 class='text-xl w-full dark:text-white py-4'>Breadcrumb</h3>

<TableProp header={propHeader} {divClass} {theadClass}>
  <TableDefaultRow {items} rowState='hover' />
</TableProp>

<h3 class='text-xl w-full dark:text-white py-4'>BreadcrumbItem</h3>

<TableProp header={propHeader} {divClass} {theadClass}>
  <TableDefaultRow items={items2} rowState='hover' />
</TableProp>