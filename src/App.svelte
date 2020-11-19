<script>
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
</script>

<style>

</style>

<main>
  <div class="grid grid-cols-10 h-screen">
    {#each filteredColors as color}
      {#each shades as shade}
        <div
          class="flex items-center justify-center {`bg-${color}-${shade}`}
          {shade > 400 ? `text-${color}-50` : `text-${color}-900`}"
          style="font-size: 0.5rem;">
          {`${color}-${shade}`}
        </div>
      {/each}
    {/each}
  </div>
</main>
