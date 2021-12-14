<!-- <script>
	export let name;
</script>

<main>
	<h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style> -->


<script>
    import {user} from "./sessionStore"
    import {supabase} from "./supabaseClient"
    import Auth from "./Auth.svelte"
    import Profile from "./Profile.svelte"

    user.set(supabase.auth.user())

    supabase.auth.onAuthStateChange((_, session) => {
        user.set(session.user)
    })
</script>

<div class="container" style="padding: 50px 0 100px 0;">
    {#if $user}
        <Profile />
    {:else}
        <Auth />
    {/if}
</div>
