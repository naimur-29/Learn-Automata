<script lang="ts">
  let { rows = $bindable(), cols = $bindable() } = $props();

  let gridLayoutOn = $state(false);

  function handleGridLayoutClick() {
    gridLayoutOn = !gridLayoutOn;
  }
</script>

<aside
  class="w-80 border-l border-white/10 bg-zinc-900 p-6 flex flex-col gap-8"
>
  <h2 class="text-xl font-bold text-white">Settings</h2>

  <section class="flex flex-col gap-4">
    <h3>
      <button
        onmousedown={handleGridLayoutClick}
        class="text-xs font-semibold uppercase tracking-wider cursor-pointer {gridLayoutOn
          ? 'text-lime-500'
          : 'text-zinc-500'}"
      >
        Grid Layout
      </button>
    </h3>

    {#if gridLayoutOn}
      <div class="flex flex-col gap-2">
        <label class="flex flex-col text-sm text-zinc-400"
          >Rows: {rows}
          <input
            type="range"
            min="2"
            max="50"
            bind:value={rows}
            class="accent-blue-500"
          />
        </label>
      </div>

      <div class="flex flex-col gap-2">
        <label class="flex flex-col text-sm text-zinc-400"
          >Columns: {cols}
          <input
            type="range"
            min="2"
            max="50"
            bind:value={cols}
            class="accent-blue-500"
          />
        </label>
      </div>
    {/if}
  </section>

  <hr class="border-white/5" />
</aside>
