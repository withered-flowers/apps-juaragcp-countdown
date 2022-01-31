<script>
  // Modified from
  // https://tailwindcomponents.com/component/countdown-timer
  import dayjs from "dayjs";

  import { onMount, onDestroy } from "svelte";
  import { fade } from "svelte/transition";
  import { eventTimeEnd } from "./configs/config.js";
  import { isCountdownEventCompleted } from "./stores/store.js";

  import FrequentlyAskedQuestions from "./FrequentlyAskedQuestions.svelte";
  import VideoIntroduction from "./VideoIntroduction.svelte";

  const endTime = eventTimeEnd;

  // "countdown" untuk nampilin halaman countdown
  // "faq" untuk menampilkan halaman FAQ
  // "video" untuk menampilkan halaman video
  let whichContentShowing = "countdown";

  let timer = null;
  let now = dayjs().valueOf();
  let end = dayjs(endTime).valueOf();

  function updateFlag(bFlag) {
    isCountdownEventCompleted.set(bFlag);
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

  function toggleContent(contentAlias) {
    whichContentShowing = contentAlias;
  }

  $: count = Math.round((end - now) / 1000);
  $: d = Math.floor(count / (3600 * 24));
  $: h = Math.floor(count / 3600) % 24;
  $: m = Math.floor(count / 60) % 60;
  $: s = count % 60;
</script>

{#if whichContentShowing === "countdown"}
  <div in:fade={{ duration: 1000 }}>
    <h1
      class="text-[#4285f4] text-[4rem] font-thin leading-[1.1] my-8 mx-auto max-w-[14rem] xs:max-w-none"
    >
      JuaraGCP Season 7 berakhir dalam
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
      (Dihitung berdasarkan waktu server Indonesia dengan waktu UTC+7)
    </p>

    <p
      class="max-w-[14rem] mt-8 mx-auto leading-[1.35] xs:max-w-none text-xl font-normal text-slate-500"
    >
      <!-- svelte-ignore a11y-invalid-attribute -->
      Belum dapat credit? Silahkan nonton
      <a
        href="#"
        class="text-[#1aa260] hover:text-[#4285f4] hover:underline"
        on:click={() => toggleContent("video")}>Video Perkenalan</a
      > ini yah.
    </p>

    <p
      class="max-w-[14rem] mt-8 mx-auto leading-[1.35] xs:max-w-none text-xl font-normal text-slate-500"
    >
      <!-- svelte-ignore a11y-invalid-attribute -->
      Ada pertanyaan? Silakan baca
      <a
        href="#"
        class="text-[#1aa260] hover:text-[#4285f4] hover:underline"
        on:click={() => toggleContent("faq")}>Pertanyaan Umum</a
      > ini dulu yah
    </p>

    <p
      class="max-w-[14rem] mt-8 mx-auto leading-[1.35] xs:max-w-none text-xl font-normal text-slate-500"
    >
      Ingin Tracking progress lab? silahkan unduh <a
        href="https://firebasestorage.googleapis.com/v0/b/dev-that-can-be-crashed.appspot.com/o/juaragcp%2FJuaraGCPSeason7Checklist.xls?alt=media&token=55680515-fcfa-4153-9d7b-87088984ebd4"
        class="text-[#1aa260] hover:text-[#4285f4] hover:underline"
        >File excel</a
      > ini.
    </p>
    <p
      class="max-w-[14rem] my-4 mx-auto leading-[1.35] xs:max-w-none text-sm font-normal text-slate-500"
    >
      (Special Thanks untuk <span class="font-bold">Yoga RSPR</span> yang sudah membuat
      file ini 😉)
    </p>

    <p
      class="max-w-[14rem] mt-8 mx-auto leading-[1.35] xs:max-w-none text-xl font-normal text-slate-500"
    >
      Ingin mengetahui sudah sampai Tier berapa? Kunjungi <a
        href="https://juaragcps7-validator.herokuapp.com/"
        class="text-[#1aa260] hover:text-[#4285f4] hover:underline"
        >Tautan ini</a
      > untuk mengetahuinya.
    </p>
    <p
      class="max-w-[14rem] my-4 mx-auto leading-[1.35] xs:max-w-none text-sm font-normal text-slate-500"
    >
      (Special Thanks untuk <span class="font-bold">Archzen</span> yang sudah melanjutkan
      situs ini 😉)
    </p>

    <p
      class="max-w-[14rem] mt-8 mx-auto leading-[1.35] xs:max-w-none text-xl font-normal text-slate-500"
    >
      Masih buntu? Yuk join grup <a
        href="https://t.me/JuaraGCP"
        class="text-[#1aa260] hover:text-[#4285f4] hover:underline"
        >telegram JuaraGCP</a
      > untuk menanyakan lebih lanjut.
    </p>
  </div>
{:else if whichContentShowing === "faq"}
  <div in:fade={{ duration: 1000 }}>
    <FrequentlyAskedQuestions />

    <!-- svelte-ignore a11y-invalid-attribute -->
    <p
      class="max-w-[14rem] mt-8 mx-auto leading-[1.35] xs:max-w-none text-xl font-normal text-slate-500"
    >
      <a
        href="#"
        class="text-[#1aa260] hover:text-[#4285f4] hover:underline"
        on:click={() => toggleContent("countdown")}>Kembali ke Countdown</a
      >
    </p>
  </div>
{:else if whichContentShowing === "video"}
  <div in:fade={{ duration: 1000 }}>
    <VideoIntroduction />

    <!-- svelte-ignore a11y-invalid-attribute -->
    <p
      class="max-w-[14rem] mt-8 mx-auto leading-[1.35] xs:max-w-none text-xl font-normal text-slate-500"
    >
      <a
        href="#"
        class="text-[#1aa260] hover:text-[#4285f4] hover:underline"
        on:click={() => toggleContent("countdown")}>Kembali ke Countdown</a
      >
    </p>
  </div>
{/if}
