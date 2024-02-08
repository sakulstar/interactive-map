<script lang="ts">
    import content from '../assets/content.json';
</script>

<main>
    {#each content["comparisons"] as comparison}
        <p class="text-orange-500 text-3xl font-semibold mt-2 ml-3">
            {comparison["title"]}
        </p>
        <div class="flex flex-row">
            <img src={comparison["image1"]} class=" w-[650px] rounded-l-lg mt-2 ml-2" alt="1" />
            <img src={comparison["image2"]} class=" w-[650px] rounded-r-lg mt-2 mr-2" alt="2" />
        </div>
    {/each}
</main>