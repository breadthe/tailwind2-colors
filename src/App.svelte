<script>
  import Footer from "./Footer.svelte";
  import { theme } from "../tailwind.config.js";

  const { colors } = { ...theme };
  const filteredColors = Object.keys(colors).filter(
    color =>
      color !== "transparent" &&
      color !== "current" &&
      color !== "black" &&
      color !== "white"
  );

  const shades = [50, 100, 200, 300, 400, 500, 600, 700, 800, 900];

  function zoom(id, direction) {
    const el = document.getElementById(id);

    if (direction === "in") {
      el.style.zIndex = 1;
      el.style.transform = "scale(2)";
      el.classList.add("shadow", "ring-4", `ring-${id}`, "ring-opacity-50");
    }

    if (direction === "out") {
      el.style.zIndex = 0;
      el.style.transform = "scale(1)";
      el.classList.remove("shadow", "ring-4", `ring-${id}`, "ring-opacity-50");
    }

    return;
  }
</script>

<style>

</style>

<main>
  <div class="grid grid-cols-10 h-screen">
    {#each filteredColors as color}
      {#each shades as shade}
        <div
          id={`${color}-${shade}`}
          class="flex items-center justify-center text-center {`bg-${color}-${shade}`}
          {shade > 400 ? `text-${color}-50` : `text-${color}-900`}"
          style="font-size: 0.5rem;"
          on:mouseover={() => zoom(`${color}-${shade}`, 'in')}
          on:mouseout={() => zoom(`${color}-${shade}`, 'out')}>
          {color} {shade}
        </div>
      {/each}
    {/each}
  </div>

  <Footer />

</main>
