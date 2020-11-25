<script>
  import Footer from "./Footer.svelte";
  import { theme } from "../tailwind.config.js";

  const { colors } = { ...theme };

  // remove non-palette colors
  ["transparent", "current", "black", "white"].forEach(c => delete colors[c]);

  const shades = [50, 100, 200, 300, 400, 500, 600, 700, 800, 900];

  function zoom(id, direction) {
    const el = document.querySelector(`#${id}`);

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

  async function copyHex(id) {
    if (!navigator.clipboard) {
      return;
    }

    try {
      // copy the hex value to the clipboard
      const hex = document.querySelector(`#hex-${id}`);
      await navigator.clipboard.writeText(hex.innerText);

      // show copied to clipboard message
      const clipMsg = document.querySelector(`#clipboardMessage`);
      clipMsg.classList.remove("hidden");
      clipMsg.classList.add("flex");

      // hide the message after x ms
      setTimeout(() => {
        clipMsg.classList.remove("flex");
        clipMsg.classList.add("hidden");
      }, 2000);
    } catch (error) {
      console.error("copy failed", error);
    }
  }
</script>

<style>

</style>

<main>
  <div id="clipboardMessage" class="fixed hidden justify-center w-full z-10">
    <div class="max-w-xs px-4 py-2 bg-black text-white ">copied!</div>
  </div>
  <div class="grid grid-cols-10 h-screen">
    {#each Object.keys(colors) as color}
      {#each shades as shade}
        <div
          id={`${color}-${shade}`}
          class="flex flex-col items-center justify-center text-center
          cursor-pointer {`bg-${color}-${shade}`}
          {shade > 400 ? `text-${color}-50` : `text-${color}-900`}"
          style="font-size: 0.5rem;"
          on:mouseover={() => zoom(`${color}-${shade}`, 'in')}
          on:mouseout={() => zoom(`${color}-${shade}`, 'out')}
          on:click={() => copyHex(`${color}-${shade}`)}>
          <span>{color} {shade}</span>
          <span id={`hex-${color}-${shade}`} style="font-size: 0.3rem;">
            {`${colors[color][shade]}`}
          </span>
        </div>
      {/each}
    {/each}
  </div>

  <Footer />

</main>
