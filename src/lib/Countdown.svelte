<script>
  // Modified from
  // https://tailwindcomponents.com/component/countdown-timer
  import dayjs from "dayjs";

  import { onMount, onDestroy } from "svelte";
  import { isCountdownCompleted } from "./stores/store.js";
  import { qwiklabsTimeEnd } from "./configs/config.js";

  const endTime = qwiklabsTimeEnd;

  let timer = null;
  let now = dayjs().valueOf();
  let end = dayjs(endTime).valueOf();

  function updateFlag(bFlag) {
    isCountdownCompleted.set(bFlag);
  }

  onMount(() => {
    if (now >= end) {
      updateFlag(true);
    }

    timer = setInterval(() => {
      now = dayjs().valueOf();

      if (now >= end) {
        updateFlag(true);
        clearInterval(timer);
      }
    }, 1000);
  });

  onDestroy(() => {
    clearInterval(timer);
  });

  $: count = Math.round((end - now) / 1000);
  $: d = Math.floor(count / (3600 * 24));
  $: h = Math.floor(count / 3600) % 24;
  $: m = Math.floor(count / 60) % 60;
  $: s = count % 60;
</script>

<h1
  class="text-[#4285f4] text-[4rem] font-thin leading-[1.1] my-8 mx-auto max-w-[14rem] xs:max-w-none"
>
  Countdown JuaraGCP Season 7
</h1>

<div class="text-6xl text-center flex w-full items-center justify-center">
  <div class="w-24 mx-1 p-2 bg-white text-[#fbbc05] rounded-lg">
    <div class="font-mono leading-none" x-text="days">{d}</div>
    <div class="font-mono uppercase text-sm leading-none">Hari</div>
  </div>
  <div class="w-24 mx-1 p-2 bg-white text-[#fbbc05] rounded-lg">
    <div class="font-mono leading-none" x-text="hours">{h}</div>
    <div class="font-mono uppercase text-sm leading-none">Jam</div>
  </div>
  <div class="w-24 mx-1 p-2 bg-white text-[#fbbc05] rounded-lg">
    <div class="font-mono leading-none" x-text="minutes">{m}</div>
    <div class="font-mono uppercase text-sm leading-none">Menit</div>
  </div>
  <div class="text-2xl mx-1 font-extralight text-slate-500">dan</div>
  <div class="w-24 mx-1 p-2 bg-white text-[#fbbc05] rounded-lg">
    <div class="font-mono leading-none" x-text="seconds">{s}</div>
    <div class="font-mono uppercase text-sm leading-none">Detik</div>
  </div>
</div>

<p
  class="max-w-[14rem] mt-8 mx-auto leading-[1.35] xs:max-w-none text-xl font-normal text-slate-500"
>
  Kunjungi <a
    href="https://goo.gle/juaragcp"
    class="text-[#1aa260] hover:text-[#4285f4] hover:underline"
    >goo.gle/juaragcp</a
  > untuk mempelajari event JuaraGCP Season 7 lebih lanjut
</p>

<p
  class="max-w-[14rem] my-4 mx-auto leading-[1.35] xs:max-w-none text-sm font-normal text-slate-500"
>
  (Dihitung berdasarkan waktu server Google Cloud Skill Boost Pukul 00.00)
</p>
