<script lang="ts">
	// This script runs both server-side (during build) and client-side
	// For a purely static page, there's no +page.ts or +page.server.ts needed
	
	let count = $state(0);
	
	function increment() {
		count++;
	}
</script>

<svelte:head>
	<title>Demo - SvelteKit Architecture</title>
	<meta name="description" content="Understanding SvelteKit's static page architecture" />
</svelte:head>

<div class="container">
	<h1>Static Page Demo</h1>
	
	<section class="architecture-info">
		<h2>How This Page Works</h2>
		<p>
			This page demonstrates SvelteKit's file-based routing. The file structure creates the route:
		</p>
		<pre><code>src/routes/demo/+page.svelte → /demo</code></pre>
		
		<h3>Key Architecture Concepts:</h3>
		<ul>
			<li><strong>+page.svelte</strong> - The page component (this file)</li>
			<li><strong>+page.ts</strong> - Optional: Load data client-side or universally</li>
			<li><strong>+page.server.ts</strong> - Optional: Load data server-side only (see /sverdle example)</li>
			<li><strong>+layout.svelte</strong> - Wraps pages (see parent routes/+layout.svelte)</li>
		</ul>
	</section>

	<section class="static-vs-dynamic">
		<h2>Static vs Dynamic</h2>
		<p>
			This page is <strong>static</strong> because:
		</p>
		<ul>
			<li>No +page.server.ts (no server-side logic)</li>
			<li>No dynamic route parameters like [id]</li>
			<li>Pre-rendered at build time by the Azure adapter</li>
			<li>Served as a plain HTML file from Azure Static Web Apps</li>
		</ul>
		<p>
			But it's still <strong>interactive</strong> thanks to Svelte's client-side hydration:
		</p>
		<div class="demo-box">
			<p>Counter: <strong>{count}</strong></p>
			<button onclick={increment}>Increment</button>
		</div>
	</section>

	<section class="routing-examples">
		<h2>Routing Examples in This App</h2>
		<table>
			<thead>
				<tr>
					<th>File Path</th>
					<th>Route</th>
					<th>Type</th>
				</tr>
			</thead>
			<tbody>
				<tr>
					<td>src/routes/+page.svelte</td>
					<td>/</td>
					<td>Static</td>
				</tr>
				<tr>
					<td>src/routes/about/+page.svelte</td>
					<td>/about</td>
					<td>Static</td>
				</tr>
				<tr>
					<td>src/routes/demo/+page.svelte</td>
					<td>/demo</td>
					<td>Static (this page)</td>
				</tr>
				<tr>
					<td>src/routes/sverdle/+page.svelte<br/>+ +page.server.ts</td>
					<td>/sverdle</td>
					<td>Server-side (game logic)</td>
				</tr>
			</tbody>
		</table>
	</section>

	<section class="next-steps">
		<h2>Try It Yourself</h2>
		<ol>
			<li>Create <code>src/routes/test/+page.svelte</code> → visit <code>/test</code></li>
			<li>Add a <code>+page.ts</code> to load data at build time</li>
			<li>Use <code>$lib</code> to import shared components: <code>import Thing from '$lib/Thing.svelte'</code></li>
			<li>Check <code>svelte.config.js</code> to see the Azure adapter configuration</li>
		</ol>
	</section>

	<nav class="demo-nav">
		<a href="/">← Home</a>
		<a href="/about">About →</a>
	</nav>
</div>

<style>
	.container {
		max-width: 800px;
		margin: 0 auto;
		padding: 2rem;
	}

	h1 {
		color: #ff3e00;
		margin-bottom: 2rem;
	}

	h2 {
		margin-top: 2rem;
		margin-bottom: 1rem;
		color: #676778;
	}

	h3 {
		margin-top: 1.5rem;
		margin-bottom: 0.5rem;
		font-size: 1.1rem;
	}

	section {
		margin-bottom: 3rem;
		padding-bottom: 2rem;
		border-bottom: 1px solid #e0e0e0;
	}

	section:last-of-type {
		border-bottom: none;
	}

	pre {
		background: #f4f4f4;
		padding: 1rem;
		border-radius: 4px;
		overflow-x: auto;
	}

	code {
		font-family: 'Fira Mono', monospace;
		font-size: 0.9em;
		background: #f4f4f4;
		padding: 0.2em 0.4em;
		border-radius: 3px;
	}

	pre code {
		background: none;
		padding: 0;
	}

	ul {
		line-height: 1.8;
	}

	ol {
		line-height: 1.8;
	}

	.demo-box {
		background: #fff4e6;
		border: 2px solid #ff3e00;
		border-radius: 8px;
		padding: 1.5rem;
		margin: 1rem 0;
		text-align: center;
	}

	.demo-box p {
		margin-bottom: 1rem;
		font-size: 1.2rem;
	}

	button {
		background: #ff3e00;
		color: white;
		border: none;
		padding: 0.75rem 1.5rem;
		border-radius: 4px;
		font-size: 1rem;
		cursor: pointer;
		transition: background 0.2s;
	}

	button:hover {
		background: #e03900;
	}

	table {
		width: 100%;
		border-collapse: collapse;
		margin: 1rem 0;
		font-size: 0.9rem;
	}

	thead {
		background: #f4f4f4;
	}

	th, td {
		padding: 0.75rem;
		text-align: left;
		border: 1px solid #e0e0e0;
	}

	th {
		font-weight: 600;
	}

	tbody tr:hover {
		background: #f9f9f9;
	}

	.demo-nav {
		display: flex;
		justify-content: space-between;
		margin-top: 3rem;
		padding-top: 2rem;
		border-top: 2px solid #ff3e00;
	}

	.demo-nav a {
		color: #ff3e00;
		text-decoration: none;
		font-weight: 600;
		padding: 0.5rem 1rem;
		border-radius: 4px;
		transition: background 0.2s;
	}

	.demo-nav a:hover {
		background: #fff4e6;
	}
</style>
