<script lang="ts">
  import { enhance } from "$app/forms";
  import IconMail from "~icons/uil/envelope";
  import IconKey from "~icons/material-symbols/key";
  import IconEye from "~icons/ph/eye-fill";
  import IconEyeSlash from "~icons/ph/eye-slash-fill";
  import IconLoader from "~icons/ri/loader-4-line";

  let hidePassword: boolean = true;
  let isLoading: boolean = false;
</script>

<div class="flex justify-center items-center h-screen">
  <form
    class="w-80 font-semibold space-y-3"
    method="POST"
    autocomplete="off"
    use:enhance={() => {
      isLoading = true;
      return async ({ update }) => {
        await update();
        isLoading = false;
      };
    }}
  >
    <h2 class="text-white text-2xl flex items-center justify-center gap-x-2">
      Create your account
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
        class="absolute left-3 top-1/2 -mt-2.5 text-slate-400 pointer-events-none peer-focus:text-blue-500 text-lg"
      />
    </div>
    <div class="relative">
      <input
        class="input pr-10 peer input-primary"
        type={hidePassword ? "password" : "text"}
        name="password"
        placeholder="Enter your password"
        required
      />
      <IconKey
        class="absolute left-3 top-1/2 -mt-2.5 text-slate-400 pointer-events-none peer-focus:text-blue-500 text-lg"
      />
      <button
        on:click={() => {
          hidePassword = !hidePassword;
        }}
        type="button"
        class="absolute right-3 top-1/2 -mt-2.5"
      >
        {#if hidePassword}
          <IconEye class="text-slate-500 cursor-pointer text-lg" />
        {:else}
          <IconEyeSlash class="text-slate-500 cursor-pointer text-lg" />
        {/if}
      </button>
    </div>
    <button class="btn-primary" type="submit">
      {#if isLoading}
        <IconLoader class="animate-spin text-lg h-5" />
      {:else}
        Sign Up
      {/if}
    </button>
    <div class="text-sm text-gray-500 flex justify-between">
      <a href="/login" class="hover:text-blue-400">Already have an account?</a>
      <a href="/terms" class="hover:text-blue-400">Terms of service</a>
    </div>
  </form>
</div>
