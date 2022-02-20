<style lang="postcss" global>
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>

<script>
import 'tw-elements';
import { onMount } from 'svelte';
import Loading from './loading.svelte';
import Author from './author.svelte';
import Error from './error.svelte';
let quote = {
    loading: false,
    author: undefined,
    en: undefined,
    error: undefined,
};

const env_variable = __api;

const endpoint = env_variable.env.API_URL_QUOTES;

onMount(async () => {
    quote.loading = true;
    try {
        const response = await fetch(endpoint);
        const data = await response.json();

        quote = {
            loading: false,
            author: data.author,
            en: data.en,
        };
    } catch (error) {
        quote = {
            loading: false,
            error: error.message,
        };
    }
});
</script>

<main class="text-center p-4 max-w-xs mx-auto sm:max-w-none">
    {#if quote.loading}
        <Loading />
    {:else if quote.error}
        <Error error="{quote.error}" />
    {:else}
        <Author name="{quote.author}" quote="{quote.en}" />
    {/if}
</main>
