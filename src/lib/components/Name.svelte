<script lang="ts">
let coordinates = $state({ x: 0, y: 0 });

function onpointermove(event: PointerEvent) {
  const target = event.currentTarget as HTMLElement;
  const rect = target.getBoundingClientRect();
  coordinates.x = (event.clientX - rect.left);
  coordinates.y = (event.clientY - rect.top);
}
</script>

<div class="stack">
  <span
    class="elsie-top"
    {onpointermove}
    aria-hidden="true"
    >
    elsie
  </span>
  <span class="elsie-bottom">
    elsie
  </span>
  <span class="elsie-glow"
  aria-hidden="true">
    elsie
  </span>
</div>

<style>

.stack {
  display: grid;
  grid-template-areas: "stack";
}

.elsie-top, .elsie-bottom, .elsie-glow {
  grid-area: stack;
  place-self: center;
	font-family: "McLaren", sans-serif;
	font-size: 8em;
	letter-spacing: clamp(0.1em, 0.34em, 0.51em);
  }

.elsie-top {
  text-shadow: 0.01em 0.015em 0em oklch(93.4% 0.0431 74.2 / 85%);
  -webkit-text-stroke: 0.015em oklch(0.541 0.1313 283.19 / 39%);
  color: oklch(19% 0.022 182);
  mix-blend-mode: difference;
}

.elsie-bottom {
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

  &:hover {
		background-image: linear-gradient(
			to bottom,
			var(--elsie-hovergold) 5%,
			var(--elsie-lightgreen) 80%
		);
		filter: blur(0.045em);
  }
}

.elsie-glow {
  color: #000;
  text-shadow:
    0.01em 0.015em 0em oklch(93.4% 0.0431 74.2 / 85%),
    calc(var(--x) * 0.004) calc(var(--y) * 0.008) 0.15em oklch(0.8848 0.0755 221.96 / 90%);
}

</style>
