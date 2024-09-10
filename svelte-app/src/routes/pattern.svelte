<script lang="ts">
  import "../styles/slots.css";
  $: value = "";
  $: proc = false;

  $: curr = "";
  $: next = "";
  $: newLine = null;
  let arr: string[] = [];

  $: lineX = 0;
  $: lineY = 0;
  let line = document.createElement("line");
  let svg = document.createElement("svg");
  let posX = 0;
  let posY = 0;
  function trace(newId: string) {
    if (proc) {
      next = newId;
      if (curr != next && !arr.includes(newId)) {
        curr = newId;
        next = curr;

        const ball = document.querySelector(`#${newId}`);
        if (ball) {
          if (!ball.classList.contains("active")) {
            ball.classList.toggle("active");
          }
        }
        arr.push(newId);
      } else {
      }
    }
  }

  function stop() {
    proc = false;
    value = "" + arr;
  }

</script>

<main
  class="main-page"
  on:mousemove={(event) => {
    lineX = event.screenX;
    lineY = event.screenY;
  }}
  draggable="false"
>
  <h1>UNLOCK ME</h1>
  <!-- svelte-ignore a11y-no-static-element-interactions -->
  <!-- svelte-ignore a11y-mouse-events-have-key-events -->
  <div
    class="unlock-pattern-container"
    on:mouseup={() => {
      stop();
      posX = 0;
      posY = 0;
    }}
    on:mousedown={() => {
      proc = true;
      posX = lineX;
      posY = lineY - 110;
    }}
  >
    {#each [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16] as i}
      <div
        class="cell-container"
        id="ball-{i}"
        on:mouseover={() => {
          trace(`ball-${i}`);
        }}
      >
        <span class="cell" id="ball-point-{i}"></span>
      </div>
    {/each}
  </div>
  <span>Code: {value}</span>
  <span>X = {lineX}</span>
  <span>Y = {lineY}</span>
</main>
