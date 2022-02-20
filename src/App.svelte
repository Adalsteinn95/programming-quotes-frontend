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
    image: undefined,
    error: undefined,
};

const env_variable = __api;

const endpoint = env_variable.env.API_URL_QUOTES;
const unsplashEndpint = env_variable.env.UNSPALSH_API_URL;
const accessKey = env_variable.env.UNSPALSH_API_ACCESS_KEY;

onMount(async () => {
    quote.loading = true;
    try {
        const response = await fetch(endpoint);
        const data = await response.json();

        const myHeaders = new Headers();
        myHeaders.append('Authorization', `Client-ID ${accessKey}`);

        const requestOptions = {
            method: 'GET',
            headers: myHeaders,
            redirect: 'follow',
        };

        const responseImage = await fetch(
            `${unsplashEndpint}/search/photos?page=1&query=${data.author}`,
            requestOptions,
        );

        const dataImage = await responseImage.json();

        quote = {
            loading: false,
            author: data.author,
            en: data.en,
            image: dataImage.results[0].urls.small,
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
        <Author
            name="{quote.author}"
            quote="{quote.en}"
            imageSrc="{quote.image}" />
    {/if}
</main>
