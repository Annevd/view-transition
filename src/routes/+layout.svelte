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

<style>

nav {
    view-transition-name: header; /* De view transition gebeud nu niet op de nav */
}

@keyframes fade-in {
	from {
		opacity: 0;
	}
}

@keyframes fade-out {
	to {
		opacity: 0;
	}
}

@keyframes slide-from-right {
	from {
		transform: translateX(30px);
	}
}

@keyframes slide-to-left {
	to {
		transform: translateX(-30px);
	}
}

:root::view-transition-old(root) {
	animation:
		90ms cubic-bezier(0.4, 0, 1, 1) both fade-out,
		300ms cubic-bezier(0.4, 0, 0.2, 1) both slide-to-left;
}

:root::view-transition-new(root) {
	animation:
		210ms cubic-bezier(0, 0, 0.2, 1) 90ms both fade-in,
		300ms cubic-bezier(0.4, 0, 0.2, 1) both slide-from-right;
}
</style>