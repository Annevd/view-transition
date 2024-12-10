<script>
    import { onNavigate } from '$app/navigation';

onNavigate((navigation) => {
	if (!document.startViewTransition) return;

	return new Promise((resolve) => {
		document.startViewTransition(async () => {
			resolve();
			await navigation.complete;
		});
	});
});
</script>

<nav>
    <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/page2">Page 2</a></li>
        <li><a href="/page3">Page 3</a></li>
    </ul>
</nav>

<slot></slot>