<script>
  import "./assets/styles.css";
  import { isCountdownCompleted } from "./lib/stores/store";
  import Countdown from "./lib/Countdown.svelte";
  import StartEvent from "./lib/StartEvent.svelte";

  let willHideCounter;

  isCountdownCompleted.subscribe((val) => {
    willHideCounter = val;
  });
</script>

<main
  class="bg-[#f1f1f1] container p-4 min-h-screen min-w-full flex flex-col items-center justify-center text-center"
>
  {#if willHideCounter}
    <Countdown />
  {:else}
    <StartEvent />
  {/if}
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  }
</style>
