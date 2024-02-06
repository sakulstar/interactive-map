<script lang="ts">
    import { BaseMap, FeatureLayer } from 'svelte-geo';
	//import germany from './assets/geojson/germany.geo.json';
    import southAndNorthKorea from './assets/geojson/southAndNorthKorea.geo.json'

    let showKorea = true;
    let showGermany = false;

    let southAndNorthKoreaSelection: any = [];

    let textElement: any;
    $:textBoxWidth = textElement ? textElement.getComputedTextLength()+10 : 0

    console.log(southAndNorthKorea["features"][0]["properties"]["name"]);
</script>

<main>
    <div class="flex flex-col items-center">
        <p class="text-orange-500 text-3xl font-semibold mt-2">
            Syd- og Nord Korea
        </p>
        <div class="rounded-lg overflow-hidden m-5 w-96 h-96 border-gray-900">
            <BaseMap background="#e0e0e0">
                <FeatureLayer 
                    geojson={southAndNorthKorea}
                    styleAccessor={(feature, selected) => ({
                        'fill': selected ? '#fc993c' : '#adadad',
                        'stroke': selected ? 'black' : 'grey',
                        'stroke-width':  1,
                        'vector-effect': 'non-scaling-stroke'
                    })}
                    selectMode={1}
                    bind:selection = {southAndNorthKoreaSelection}
                />
            </BaseMap>
        </div>
    </div>
</main>