<script>
  import "./assets/styles.css";
  import Countdown from "./lib/Countdown.svelte";
</script>

<main
  class="bg-[#f1f1f1] container p-4 min-h-screen min-w-full flex flex-col items-center justify-center text-center"
>
  <Countdown />
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
  }
</style>
