<script lang="ts">

let coords = $state({
  glowX: 0,
  glowY: 0,
  gradX: -333,
  gradY: -333
});

// let isAnimating = $state(false);

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

// function triggerAnimation() {
//   isAnimating = true;
//   setTimeout(() => (isAnimating = false), 500);
// }

</script>

<button class="elsie-stack"
  style="--gradX: {coords.gradX}px; --gradY: {coords.gradY}px; --glowX: {coords.glowX}rem; --glowY: {coords.glowY}rem"
  {onpointermove}
  {onpointerleave}
  >

  <span class="elsie-stack glow"
    aria-hidden="true">
    elsie
  </span>

  <a class="elsie-stack bottom"
  href="https://github.com/els-ie"
  aria-label="Check out my GitHub"
  draggable="false"
  >
    elsie
  </a>

  <span
    class="elsie-stack top"
    aria-hidden="true"
    >
    elsie
  </span>
</button>

<style>

.elsie-stack {
  display: grid;
  grid-template-areas: "stack";
  text-align: center;

  @media (prefers-reduced-motion: no-preference) {
    &:active { animation: elsie-click-animation 1s ease-in-out;}
  }
}

.elsie-stack.top, .elsie-stack.bottom, .elsie-stack.glow {
  grid-area: stack;
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
  background: radial-gradient(
      circle 1.5em at calc(50% + var(--gradX, 0em)) calc(50% + var(--gradY, 0em)),
      oklch(85.1% 0.0448 283.2) 0%,
      oklch(54.1% 0.1313 283.2) 100%
  );
  text-shadow: .012em .018em 0em oklch(93.4% 0.0431 74.2);
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-stroke: .021em transparent;
  color: oklch(19% 0.022 182);
  pointer-events: none;
  user-select: none;
  -webkit-user-select: none;
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
  color: oklch(0.8848 0.0755 221.96 / 20%);
  filter: blur(.08em);
  user-select: none;
  -webkit-user-select: none;

  @media (prefers-reduced-motion: no-preference) {
  translate: calc(var(--glowX) * -.004) calc(var(--glowY) * -.012);
  transition: translate .09s linear;
  }
}

button {
  background-color: transparent;
  border: transparent;
}

a {
    text-decoration: none;
}

@keyframes elsie-click-animation {
  0%, 100% { transform: scale(1);}
  25% { transform: scale(0.9);}
  75% { transform: scale(0.2);}
}
</style>
