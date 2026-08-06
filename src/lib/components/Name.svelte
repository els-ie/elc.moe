<script lang="ts">

let coords = $state({
  glowX: 0,
  glowY: 0,
  gradX: -333,
  gradY: -333
});

function onpointermove(event: PointerEvent) {
  const target = event.currentTarget as HTMLElement;
  const rect = target.getBoundingClientRect();
  coords.glowX = event.clientX - rect.left - rect.width / 2;
  coords.glowY = event.clientY - rect.top - rect.height / 2;
  coords.gradX = event.clientX - rect.left - rect.width / 2;
  coords.gradY = event.clientY - rect.top - rect.height / 2;
}

function onpointerleave() {
  coords.glowX = 0
  coords.glowY = 0
  coords.gradX = -333
  coords.gradY = -333
}

</script>

<div class="elsie-stack"
    style="--gradX: {coords.gradX}px; --gradY: {coords.gradY}px; --glowX: {coords.glowX}rem; --glowY: {coords.glowY}rem"
    {onpointermove}
    {onpointerleave}
    aria-hidden="true">
  <span class="elsie-stack glow"
    aria-hidden="true">
    elsie
  </span>
  <span class="elsie-stack bottom">
    elsie
  </span>
  <span
    class="elsie-stack top"
    aria-hidden="true"
    >
    elsie
  </span>
</div>

<style>

.elsie-stack {
  display: grid;
  grid-template-areas: "stack";
}

.elsie-stack.top, .elsie-stack.bottom, .elsie-stack.glow {
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

.elsie-stack.top {
  text-shadow: .01em .015em 0em oklch(93.4% 0.0431 74.2 / 85%);
  background: radial-gradient(
      circle 1.5em at calc(50% + var(--gradX, 0em)) calc(50% + var(--gradY, 0em)),
      oklch(85.1% 0.0448 283.2) 0%,
      oklch(54.1% 0.1313 283.2) 100%
  );
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-stroke: .025em transparent;
  color: oklch(19% 0.022 182);
  pointer-events: none;
}

.elsie-stack.bottom {
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

.elsie-stack.glow {
  place-items: center;
  color: oklch(0.8848 0.0755 221.96 / 20%);
  filter: blur(.08em);

  @media (prefers-reduced-motion: no-preference) {
  translate: calc(var(--glowX) * -.004) calc(var(--glowY) * -.012);
  transition: translate .09s linear;
  }
}

</style>
