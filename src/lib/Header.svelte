<script lang="ts">
	let isOpen = $state(false);

	function toggleMenu() {
		isOpen = !isOpen;
	}
</script>

<div>
	<div id="menu-bar" class="relative bg-white px-4 py-2 shadow-sm md:px-8">
		<div class="flex items-center justify-between">
			<a href="/natura/" class="shrink-0">
				<img src="/natura/icon.jpeg" alt="Natura icon" class="h-16 w-16 object-cover" />
			</a>

			<button
				onclick={toggleMenu}
				class="block p-2 text-gray-600 hover:text-black focus:outline-none md:hidden"
				aria-label="Toggle menu"
				aria-expanded={isOpen}
			>
				<svg
					class="h-6 w-6 transition-transform duration-200"
					fill="none"
					stroke="currentColor"
					viewBox="0 0 24 24"
				>
					{#if isOpen}
						<!-- "X" Close Icon -->
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M6 18L18 6M6 6l12 12"
						/>
					{:else}
						<!-- Hamburger Lines -->
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M4 6h16M4 12h16M4 18h16"
						/>
					{/if}
				</svg>
			</button>

			<nav class="hidden gap-8 font-mono font-bold md:flex">
				<a href="#learn-more" class="hover:text-emerald-600 transition-colors">Learn</a>
				<a href="#sim" class="hover:text-emerald-600 transition-colors">Simulator</a>
			</nav>
		</div>

		{#if isOpen}
			<nav
				class="absolute left-0 right-0 top-full z-50 border-t border-gray-100 bg-white py-4 font-mono font-bold shadow-lg transition-all md:hidden"
			>
				<div class="flex flex-col items-center gap-4">
					<a
						href="#learn-more"
						onclick={toggleMenu}
						class="w-full py-2 text-center hover:bg-gray-50 hover:text-emerald-600"
					>
						Learn
					</a>
					<a
						href="#sim"
						onclick={toggleMenu}
						class="w-full py-2 text-center hover:bg-gray-50 hover:text-emerald-600"
					>
						Simulator
					</a>
				</div>
			</nav>
		{/if}
	</div>
	<br />
</div>