<script lang="ts">
  let m = $state({ x: 0, y: 0 });

  function handleMousemove(event) {
    m.x = event.clientX;
    m.y = event.clientY;
  }
</script>

<!-- <video -->
<!--   src={stars} -->
<!--   class="absolute w-screen mix-blend-screen -z-9" -->
<!--   muted -->
<!--   autoplay -->
<!--   loop -->
<!-- ></video> -->
<!---->
<!-- <div class="bg-custom-radial w-dvw h-dvh -z-10"></div> -->

<!-- svelte-ignore a11y_no_static_element_interactions -->

<body>
  <main class="flex flex-col min-h-screen">
    <!-- <div class="absolute gradient-circle"></div> -->
    <div class="flex flex-col justify-center">
      <!-- Elsie  -->
      <div
        class="relative min-h-200 flex justify-center pt-10 md:justify-start md:pt-65 md:pl-72 z-10"
      >
        <div
          class="elsie-text mix-blend-screen hollow-text select-none"
          aria-hidden="true"
        >
          elsie
        </div>

        <div
          class="elsie-text mix-blend-color-dodge [text-shadow:1px_2px_0px_oklch(0.8812_0.0732__59.26/80%)] select-none"
          aria-hidden="true"
        >
          elsie
        </div>

        <div
          class="elsie-text text-transparent bg-clip-text bg-linear-to-b mix-blend-lighten to-elsielightgreen
        from-49% from-elsiedarkgreen hover:from-elsiehovergold
        hover:from-5% hover:to-80%"
          style="filter:blur(6px)"
        >
          elsie
        </div>
      </div>
    </div>
  </main>
</body>

<style>
</style>
