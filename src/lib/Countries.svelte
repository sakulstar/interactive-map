<script lang="ts">
    import { BaseMap, FeatureLayer } from 'svelte-geo';
	import germany from '../assets/geojson/germany.geo.json';
    import korea from '../assets/geojson/korea.geo.json';
    import content from '../assets/content.json';

    let toggleCountry = true;

    let koreaSelection: any = [];
    let germanySelection: any = [];

    let koreaID: number;
    let germanyID: number;

    $:koreaID = koreaSelection[0]
    $:germanyID = germanySelection[0]

    $:console.log("KoreaID: " + (koreaID - 1));
    $:console.log("GermanyID: " + (germanyID - 1))
</script>

<main>
    <!-- South and North Korea -->
    {#if toggleCountry}
    <div class="flex flex-row">
        <div class="text-center">
            <p class="text-orange-500 text-3xl font-semibold mt-2">
                Syd- og Nord Korea
            </p>
            <div class="rounded-lg overflow-hidden m-5 w-96 h-96 border-gray-900">
                <BaseMap background="#e0e0e0">
                    <FeatureLayer 
                        geojson={korea}
                        styleAccessor={(feature, selected) => ({
                            'fill': selected ? '#fc993c' : '#adadad',
                            'stroke': selected ? 'black' : 'grey',
                            'stroke-width':  1,
                            'vector-effect': 'non-scaling-stroke'
                        })}
                        selectMode={1}
                        idAccessor={(feature) => feature.properties.country_id}
                        bind:selection = {koreaSelection}
                    />
                </BaseMap>
            </div>
            <div class="flex flex-row ml-5 text-gray-900 font-medium select-none">
                <label for="koreaRadioButton" class="mr-5">
                    <input id=koreaRadioButton name="countryToggle" type="radio" value={true} bind:group={toggleCountry} />
                    Vis Korea
                </label><br>
                <label for="germanyRadioButton">
                    <input id="germanyRadioButton" name="countryToggle" type="radio" value={false} bind:group={toggleCountry} />
                    Vis Tyskland
                </label>
            </div>
        </div>
        <div class="flex flex-col">
            <p class="text-orange-500 text-3xl font-semibold mt-2 mb-5">
                {!koreaID ? 'Vælg et land' : content["countries"]["korea"][koreaID - 1]["title"]}
            </p>
            <p class="text-gray-900 text-wrap max-w-[900px]">
                {!koreaID ? '' : content["countries"]["korea"][koreaID - 1]["description"]}
            </p>
            {#if koreaID}
                <ul class="ml-4 list-disc">
                    {#each content["countries"]["korea"][koreaID - 1]["list"] as list}
                        <li>{list}</li>
                    {/each}
                </ul>
            {/if}
        </div>
    </div>
    {/if}
    <!-- West and East Germany -->
    {#if !toggleCountry}
    <div class="flex flex-row">
        <div class="text-center">
            <p class="text-orange-500 text-3xl font-semibold mt-2">
                Vest- og Østtyskland
            </p>
            <div class="rounded-lg overflow-hidden m-5 w-96 h-96 border-gray-900">
                <BaseMap background="#e0e0e0">
                    <FeatureLayer 
                        geojson={germany}
                        styleAccessor={(feature, selected) => ({
                            'fill': selected ? '#fc993c' : '#adadad',
                            'stroke': selected ? 'black' : 'grey',
                            'stroke-width':  1,
                            'vector-effect': 'non-scaling-stroke'
                        })}
                        idAccessor={(feature) => feature.properties.country_id}
                        selectMode={1}
                        bind:selection = {germanySelection}
                    />
                </BaseMap>
            </div>
            <div class="flex flex-row ml-5 text-gray-900 font-medium select-none">
                <label for="koreaRadioButton" class="mr-5">
                    <input id=koreaRadioButton name="countryToggle" type="radio" value={true} bind:group={toggleCountry} />
                    Vis Korea
                </label><br>
                <label for="germanyRadioButton">
                    <input id="germanyRadioButton" name="countryToggle" type="radio" value={false} bind:group={toggleCountry} />
                    Vis Tyskland
                </label>
            </div>
        </div>
        <div class="flex flex-col">
            <p class="text-orange-500 text-3xl font-semibold mt-2 mb-5">
                {!germanyID ? 'Vælg et land' : content["countries"]["germany"][germanyID - 1]["title"]}
            </p>
            <div class="text-gray-900 text-wrap max-w-[900px] mb-2">
                {!germanyID ? '' : content["countries"]["germany"][germanyID - 1]["description"]}
            </div>
            {#if germanyID}
                <ul class="ml-4 list-disc text-gray-900">
                    {#each content["countries"]["germany"][germanyID - 1]["list"] as list}
                        <li>{list}</li>
                    {/each}
                </ul>
            {/if}
        </div>
    </div>
    {/if}
</main>