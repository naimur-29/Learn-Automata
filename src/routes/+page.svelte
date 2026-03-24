<script lang="ts">
  import Canvas from "$lib/Canvas.svelte";
  import Sidebar from "$lib/Sidebar.svelte";

  // Central State
  let rows = $state(10);
  let cols = $state(10);
</script>

<div class="flex h-screen w-full bg-zinc-950 text-zinc-100 overflow-hidden">
  <main class="flex-1 flex items-center justify-center p-8">
    <Canvas {rows} {cols} />
  </main>

  <Sidebar bind:rows bind:cols />
</div>
