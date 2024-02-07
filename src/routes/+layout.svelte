<script>
	import { page } from '$app/stores';
    import "../app.pcss";
</script>

<h1 class="text-5xl">EDAR 2024</h1>

<nav>
	<a href="/" aria-current={$page.url.pathname === '/'}>
		home
	</a>

	<a href="/ourbooks" aria-current={$page.url.pathname === '/ourbooks'}>
		our "books"
	</a>

    <a href="/eventdetails" aria-current={$page.url.pathname === '/eventdetails'}>
		event details
	</a>

    <a href="/booking" aria-current={$page.url.pathname === '/booking'}>
		booking
	</a>
</nav>

<slot />
