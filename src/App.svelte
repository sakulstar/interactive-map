<script lang="ts">
    import { BaseMap, FeatureLayer } from 'svelte-geo';
	import germany from './assets/geojson/germany.geo.json';
    import korea from './assets/geojson/korea.geo.json';
    import content from './assets/content.json';

    let toggleCountry = true;

    let koreaSelection: any = [];
    let germanySelection: any = [];

    let koreaSelectionString: string = String(koreaSelection);

    const countries = {
        "northKorea": {
            "title": "North Korea",
            "description": "This is the description for North Korea"
        },
        "southKorea": {
            "title": "South Korea",
            "description": "This is the description for South Korea"
        },
        "eastGermany": {
            "title": "East Germany",
            "description": "This is the description for East Germany"
        },
        "westGermany": {
            "title": "West Germany",
            "description": "This is the description for West Germany"
        }
    } 
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
                        idAccessor={(feature) => feature.properties.country_name}
                        bind:selection = {koreaSelection}
                    />
                </BaseMap>
            </div>
            <div class="flex flex-row ml-5 text-gray-900 font-medium select-none">
                <p class="mr-5">
                    <input name="countryToggle" type="radio" value={true} bind:group={toggleCountry} />
                    Show Korea
                </p><br>
                <p>
                    <input name="countryToggle" type="radio" value={false} bind:group={toggleCountry} />
                    Show Germany
                </p>
            </div>
        </div>
        <div class="flex flex-col">
            <p class="text-orange-500 text-3xl font-semibold mt-2 mb-5">
                {countries["northKorea"]["title"]}
            </p>
            <p class="text-gray-900 text-wrap max-w-[900px]">
                {content["northKorea"]["description"]}
            </p>
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
                        selectMode={1}
                        bind:selection = {germanySelection}
                    />
                </BaseMap>
            </div>
            <div class="flex flex-row ml-5 text-gray-900 font-medium select-none">
                <p class="mr-5">
                    <input name="countryToggle" type="radio" value={true} bind:group={toggleCountry} />
                    Show Korea
                </p><br>
                <p>
                    <input name="countryToggle" type="radio" value={false} bind:group={toggleCountry} />
                    Show Germany
                </p>
            </div>
        </div>
        <div class="flex flex-col">
            <p class="text-orange-500 text-3xl font-semibold mt-2 mb-5">
                Title
            </p>
            <p class="text-gray-900 text-wrap max-w-[900px]">
                Description
            </p>
        </div>
    </div>
    {/if}
</main>