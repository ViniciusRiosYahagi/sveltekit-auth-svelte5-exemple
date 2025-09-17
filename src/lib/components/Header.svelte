<script lang="ts">
	import { page } from '$app/state';
	import { signIn, signOut } from '@auth/sveltekit/client';

  let user = $derived(page.data.session?.user)
  let session = $derived(page.data.session)
</script>

<header class="p-10">
	<div class="flex items-center justify-between bg-amber-100 p-5">
		<img
			alt="User avatar"
			src={user?.image ??
				`https://api.dicebear.com/9.x/thumbs/svg?seed=${Math.floor(Math.random() * 100000) + 1}&randomizeIds=true`}
			class="size-15 rounded-full"
		/>
		<div>
			{#if session}
				<span class="signedInText pr-3">
					{user?.email ?? user?.name}
				</span>
				<button class="bg-blue-400 p-3" onclick={() => signOut()}>Sign in</button>
			{:else}
				<span class="notSignedInText pr-4">You are not signed in</span>
				<button class="bg-blue-400 p-3" onclick={() => signIn()}>Sign in</button>
			{/if}
		</div>
	</div>
	<nav>
		<ul class="flex gap-3">
			<li class="text-blue-500 underline"><a href="/">Home</a></li>
			<li class="text-blue-500 underline"><a href="/protected">Protected</a></li>
		</ul>
	</nav>
</header>
