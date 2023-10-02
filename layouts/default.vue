<template>
	<h1>Layout default</h1>
	<nav>
		<NuxtLink to="/">Home</NuxtLink>
		<NuxtLink to="/calculator">Calculator</NuxtLink>
	</nav>
	<main>
		<slot />
	</main>
</template>
<style scoped lang="scss">
nav {
	display: flex;
	justify-content: center;
	gap: 2rem;
	font-size: 2rem;
	overflow-x: scroll;
	width: 100%;
	@extend %disable-scrollbar;
}

main {
	margin-top: 2rem;
}
</style>