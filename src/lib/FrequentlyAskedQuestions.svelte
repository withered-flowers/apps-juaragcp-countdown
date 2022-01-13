<script>
  import { faq } from "./configs/config.js";
</script>

<h1
  class="text-[#4285f4] text-[3rem] font-thin leading-[1.1] my-8 mx-auto max-w-[14rem] xs:max-w-none"
>
  Pertanyaan Umum
</h1>

<div class="flex flex-col text-left font-mono divide-y-4 max-w-4xl">
  {#each faq as question}
    <div class="px-2 py-4">
      <p class="text-slate-500">
        <span class="text-2xl mr-4">Q</span>{question.q}
      </p>
      <p class="text-slate-500">
        <span class="text-2xl mr-4">A</span>{question.a}
      </p>
    </div>
  {/each}
</div>
