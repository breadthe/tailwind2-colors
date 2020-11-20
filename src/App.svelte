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

  <footer
    class="bg-gradient-to-r flex from-indigo-700 justify-center p-8 space-x-8
    text-rose-100 to-rose-900">

    <div class="relative group">
      <a
        href="https://tailwindcss.com/"
        title="TailwindCSS 2.0 color palette"
        class="relative">
        TailwindCSS
        <span
          class="absolute bg-rose-300 group-hover:bg-rose-500 left-0 opacity-50
          pb-2 top-4 sm:top-2/3 w-full" />
      </a>
      2.0 color palette
    </div>

    <div class="flex space-x-2 group">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        fill="currentColor"
        class="text-rose-100"
        viewBox="0 0 24 24">
        <path
          d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205
          11.385.6.113.82-.258.82-.577
          0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07
          3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838
          1.236 1.838 1.236 1.07 1.835 2.809 1.305
          3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93
          0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0
          1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405
          2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84
          1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81
          2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092
          24 17.592 24 12.297c0-6.627-5.373-12-12-12" />
      </svg>
      <a href="https://github.com/breadthe/tailwind2-colors" class="relative">
        GitHub
        <span
          class="absolute bg-rose-300 group-hover:bg-rose-500 left-0 opacity-50
          pb-2 top-4 sm:top-2/3 w-full" />
      </a>
    </div>

    <div class="flex space-x-2 group">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        viewBox="0 0 24 24"
        fill="none"
        stroke="currentColor"
        stroke-width="2"
        stroke-linecap="round"
        stroke-linejoin="round"
        class="feather feather-twitter">
        <path
          d="M23 3a10.9 10.9 0 0 1-3.14 1.53 4.48 4.48 0 0 0-7.86 3v1A10.66
          10.66 0 0 1 3 4s-4 9 5 13a11.64 11.64 0 0 1-7 2c9 5 20 0 20-11.5a4.5
          4.5 0 0 0-.08-.83A7.72 7.72 0 0 0 23 3z" />
      </svg>
      <a href="https://twitter.com/brbcoding" class="relative">
        @brbcoding
        <span
          class="absolute bg-rose-300 group-hover:bg-rose-500 left-0 opacity-50
          pb-2 top-4 sm:top-2/3 w-full" />
      </a>
    </div>
  </footer>
</main>
