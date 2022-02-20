<script>
export let name;
export let quote;
export let imageSrc;
</script>

<div class="min-h-screen bg-gray-200 flex justify-center items-center">
    <div
        class="max-w-2xl bg-white border-2 border-gray-300 p-5 rounded-md tracking-wide shadow-lg">
        <div id="header" class="flex">
            <img
                alt="author images"
                class="w-45 rounded-md border-2 border-gray-300"
                src="{imageSrc}" />
            <div id="body" class="flex flex-col ml-5">
                <h4 id="name" class="text-xl font-semibold mb-2">{quote}</h4>
                <div class="flex mt-5">
                    <p class="ml-3">{name}</p>
                </div>
            </div>
        </div>
    </div>
</div>
