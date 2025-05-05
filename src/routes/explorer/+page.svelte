<script lang="ts">
  import { currentIsland, currentView, markerSelected } from '$lib/runes.svelte';
  import { oileainService } from '$lib/services/oileain-service';
  import { generateMarkerSpec } from '$lib/services/oileain-utils';
  import IslandDescription from '$lib/ui/IslandDescription.svelte';
  import IslandLatLng from '$lib/ui/IslandLatLng.svelte';
  import LeafletMap from '$lib/ui/LeafletMap.svelte';
  import type { PageProps } from './$types';
  let { data }: PageProps = $props();
  let navigator: LeafletMap;

  currentView.value = 'Explorer';

  $effect(() => {
    if (markerSelected.value) {
      oileainService.getIslandById(markerSelected.value.id).then((result) => {
        currentIsland.value = result;
        navigator.addPopupMarkerAndZoom('selected', generateMarkerSpec(result));
      });
    }
  });
</script>

<div class="columns">
  <div class="column has-text-centered">
    <LeafletMap id="map-main" zoom={7} height={60} markerLayers={data.markerLayers} />
    {#if currentIsland.value}
      <IslandLatLng island={currentIsland.value} />
    {/if}
  </div>
  <div class="column">
    <LeafletMap id="map-secondary" height={30} activeLayer="Satellite" bind:this={navigator} />
    {#if currentIsland.value}
      <IslandDescription island={currentIsland.value} />
    {/if}
  </div>
</div>
