<script lang="ts">
let coordinates = $state({ x: 0, y: 0 });

function onpointermove(event: PointerEvent) {
  const target = event.currentTarget as HTMLElement;
  const rect = target.getBoundingClientRect();
  coordinates.x = (event.clientX - rect.left);
  coordinates.y = (event.clientY - rect.top);
}

function onpointerleave() {
  coordinates.x = 0;
  coordinates.y = 0;
}
</script>

<div>
  <span
    class="elsie-header"
    {onpointermove}
    {onpointerleave}
    style="--x: {coordinates.x}rem; --y: {coordinates.y}rem"
    aria-hidden="true"
    >
  </span>
</div>

<style>
.elsie-header {
	--text: "elsie";
	position: relative;
  display: grid;
  place-items: center;
	font-family: "McLaren", sans-serif;
	font-size: 8em;
	line-height: 1;
	letter-spacing: var(--tracking, 0.1em);
	@media screen and (min-width: 768px) {
		--tracking: 0.34em;
	}
  
  @media (prefers-reduced-motion: no-preference) {
    transition: letter-spacing 0.2s ease-in;
  }

	&::before {
		position: absolute;
		content: var(--text);
		text-shadow: 0.01em 0.015em 0em oklch(93.4% 0.0431 74.2 / 85%);
		-webkit-text-stroke: 0.015em oklch(0.541 0.1313 283.19 / 39%);
		color: oklch(19% 0.022 182);
		mix-blend-mode: difference;
	}

	&::after {
		position: absolute;
		content: var(--text);
		background-clip: text;
    -webkit-background-clip: text;
		background-image: linear-gradient(
			to bottom,
			var(--elsie-darkgreen) 49%,
			var(--elsie-lightgreen)
		);
		color: transparent;
		mix-blend-mode: lighten;
		filter: blur(0.04em);
	}

	&:hover::before {
		text-shadow:
			0.01em 0.015em 0em oklch(93.4% 0.0431 74.2 / 85%),
			calc(var(--x) * -0.0045) calc(var(--y) * -0.012) 0.15em oklch(0.8848 0.0755 221.96 / 20%);

	}

	&:hover::after {
		background-image: linear-gradient(
			to bottom,
			var(--elsie-hovergold) 5%,
			var(--elsie-lightgreen) 80%
		);
		filter: blur(0.045em);
	}
}
</style>
