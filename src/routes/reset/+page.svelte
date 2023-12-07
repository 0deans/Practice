<script lang="ts">
  import IconMail from "~icons/uil/envelope";
  import IconLoader from "~icons/ri/loader-4-line";

  let isLoading: boolean = false;
</script>

<div class="flex justify-center items-center h-screen">
  <form class="w-80 font-semibold space-y-3"     
  use:enhance={() => {
    isLoading = true;
    return async ({ update }) => {
      await update();
      isLoading = false;
    };
  }}>
    <h2 class="text-white text-2xl flex items-center justify-center gap-x-2">
      Reset your password
    </h2>
    <div class="relative">
      <input
        class="input peer input-primary"
        type="email"
        name="email"
        placeholder="Enter your email address"
        required
      />
      <IconMail
        class="absolute left-3 top-1/2 -mt-2.5 text-slate-400 pointer-events-none
         peer-focus:text-blue-500 text-lg"
      />
    </div>
    <button class="btn-primary" type="submit">
      {#if isLoading}
        <IconLoader class="animate-spin text-lg h-5" />
      {:else}
        Send password reset email
      {/if}
    </button>
  </form>
</div>
