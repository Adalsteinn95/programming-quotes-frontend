<script>
export let name;
export let quote;
</script>

<div
    class="min-w-screen min-h-screen bg-red-200 flex items-center justify-center px-5 py-5"
    style="min-height: 100vh">
    <div
        class="w-full mx-auto rounded-lg bg-white shadow-lg px-5 pt-5 pb-10 text-gray-800"
        style="max-width: 500px">
        <div class="w-full mb-10">
            <div class="text-3xl text-blue-500 text-left leading-tight h-3">
                “
            </div>
            <p class="text-sm text-gray-600 text-center px-5">{quote}</p>
            <div
                class="text-3xl text-blue-500 text-right leading-tight h-3 -mt-3">
                ”
            </div>
        </div>
        <div class="w-full">
            <p class="text-md text-blue-500 font-bold text-right">{name}</p>
        </div>
    </div>
</div>
