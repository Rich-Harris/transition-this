<nav>
	<a href="/teal">teal</a>
	<a href="/goldenrod">goldenrod</a>
	<a href="/hotpink">hotpink</a>
</nav>

<main>
	<slot />
</main>

<style>
	:root {
		font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu,
			Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
	}

	nav {
		display: flex;
		justify-content: center;
		gap: 0.5em;
	}

	main {
		width: 100vw;
		height: 100vh;
		display: flex;
		flex-direction: column;
	}
</style>
