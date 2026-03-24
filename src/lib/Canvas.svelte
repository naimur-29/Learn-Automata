<script lang="ts">
  let { rows, cols } = $props(); // Svelte 5 runes
  let canvas: HTMLCanvasElement;
  let mouseX = -100;
  let mouseY = -100;

  $effect(() => {
    const ctx = canvas.getContext("2d")!;
    let frame: number;

    const render = () => {
      const cellW = canvas.width / cols;
      const cellH = canvas.height / rows;

      ctx.fillStyle = "#18181b";
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      for (let r = 0; r < rows; r++) {
        for (let c = 0; c < cols; c++) {
          const x = c * cellW;
          const y = r * cellH;
          const isHovered =
            mouseX >= x &&
            mouseX < x + cellW &&
            mouseY >= y &&
            mouseY < y + cellH;

          if (isHovered) {
            ctx.fillStyle = "#3b82f6";
            ctx.shadowBlur = 15;
            ctx.shadowColor = "#3b82f6";
          } else {
            ctx.fillStyle = "transparent";
            ctx.shadowBlur = 0;
          }
          ctx.fillRect(x + 1, y + 1, cellW - 2, cellH - 2);
          ctx.strokeStyle = "rgba(255, 255, 255, 0.1)";
          ctx.strokeRect(x, y, cellW, cellH);
        }
      }
      frame = requestAnimationFrame(render);
    };

    render();
    return () => cancelAnimationFrame(frame);
  });

  const handleMouseMove = (e: MouseEvent) => {
    const rect = canvas.getBoundingClientRect();
    mouseX = e.clientX - rect.left;
    mouseY = e.clientY - rect.top;
  };
</script>

<canvas
  bind:this={canvas}
  onmousemove={handleMouseMove}
  onmouseleave={() => {
    mouseX = -100;
    mouseY = -100;
  }}
  width="600"
  height="600"
  class="border border-white/10 rounded-xl bg-zinc-950 shadow-2xl"
></canvas>
