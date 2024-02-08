<script lang="ts">
    import Countries from "./lib/Countries.svelte";
    import Comparisons from "./lib/Comparisons.svelte";

    let toggleTab = false;
</script>

<main class="relative">
    <div class="flex flex-row ml-5 text-gray-900 font-medium select-none absolute top-1 right-1">
        <label for="contriesRadioButton" class="mt-2 py-1 px-2 text-white font-semibold rounded-lg {toggleTab ? 'bg-orange-500' : 'bg-orange-500/50'}">
            <input id=contriesRadioButton name="tabToggle" type="radio" value={true} bind:group={toggleTab} class="hidden" />
            Lande
        </label><br>
        <label for="comparisonsRadioButton" class="mx-4 mt-2 py-1 px-2 text-white font-semibold rounded-lg {!toggleTab ? 'bg-orange-500' : 'bg-orange-500/50'}">
            <input id="comparisonsRadioButton" name="tabToggle" type="radio" value={false} bind:group={toggleTab} class="hidden" />
            Sammenligninger
        </label>
    </div>
    {#if toggleTab}
        <Countries />
    {/if}
    {#if !toggleTab}
        <Comparisons />
    {/if}
</main>