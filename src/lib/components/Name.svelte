<script lang="ts">
import { Spring } from 'svelte/motion';

let coordinates = $state({ x: 0, y: 0 });

function onpointermove(event: PointerEvent) {
  const target = event.currentTarget as HTMLElement;
  const rect = target.getBoundingClientRect();
  coordinates.x = event.clientX - rect.left - rect.width / 2;
  coordinates.y = event.clientY - rect.top - rect.height / 2;
}

function onpointerleave() {
  coordinates.x = 0
  coordinates.y = 0
}

</script>

<div class="smol-stack"
    style="--x: {coordinates.x}rem; --y: {coordinates.y}rem"
    {onpointermove}
    {onpointerleave}
    aria-hidden="true">
  <top
    class="elsie-top"
    aria-hidden="true"
    >
    elsie
  </top>
  <bottom class="elsie-bottom">
    elsie
  </bottom>
  <glow class="elsie-glow"
    aria-hidden="true">
    elsie
  </glow>
</div>

<style>

.smol-stack {
  display: grid;
  grid-template-areas: "stack";
}

.smol-stack > * {
  grid-area: stack
}
.smol-stack top, .smol-stack bottom, .smol-stack glow {
  grid-area: stack;
  place-self: center;
  font-family: "McLaren", sans-serif;
  font-size: 8em;
  letter-spacing: var(--tracking, .15em);

  @media (prefers-reduced-motion: no-preference) {
    transition: letter-spacing .16s ease-out;
  }

  @media screen and (min-width: 768px) {
    --tracking: .34em;
  }

  }

.elsie-top {
  text-shadow: .01em .015em 0em oklch(93.4% 0.0431 74.2 / 85%);
  background: conic-gradient(from 10deg, oklch(0.541 0.1313 283.19 / 39%), white);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-stroke: .015em transparent;
  color: oklch(19% 0.022 182);
  pointer-events: none
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
  filter: blur(.04em);

  &:hover {
		background-image: linear-gradient(
			to bottom,
			var(--elsie-hovergold) 5%,
			var(--elsie-lightgreen) 80%
		);
		filter: blur(.045em);
  }
}

.elsie-glow {
  color: #000;

  @media (prefers-reduced-motion: reduce) {
  text-shadow:
    .01em .015em 0em oklch(93.4% 0.0431 74.2 / 85%),
    0em 0em .15em oklch(0.8848 0.0755 221.96 / 30%);
  }

  @media (prefers-reduced-motion: no-preference) {
  text-shadow:
    .01em .015em 0em oklch(93.4% 0.0431 74.2 / 85%),
    calc(var(--x) * -.0045) calc(var(--y) * -.008) .15em oklch(0.8848 0.0755 221.96 / 30%);
  }
  mix-blend-mode: linear-dodge;

}

</style>
