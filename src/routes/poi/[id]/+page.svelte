<script lang="ts">
  import IslandCoordinates from '$lib/ui/IslandCoordinates.svelte';
  import IslandDescription from '$lib/ui/IslandDescription.svelte';
  import LeafletMap from '$lib/ui/LeafletMap.svelte';
  import type { PageProps } from './$types';
  let { data }: PageProps = $props();
  import { currentIsland, currentView } from '$lib/runes.svelte';
  import { oileainService } from '$lib/services/oileain-service';
  import { page } from '$app/state';
  import { generateMarkerSpec } from '$lib/services/oileain-utils';

  let mapTerrain: LeafletMap;
  currentIsland.value = data.island;
  currentView.value = 'Wanderer';

  $effect(() => {
    oileainService.getIslandById(page.params.id).then((result) => {
      currentIsland.value = data.island;
      mapTerrain?.addPopupMarkerAndZoom('selected', generateMarkerSpec(result));
    });
  });
</script>

<div class="columns">
  <div class="column">
    <LeafletMap id="map-main" marker={data.marker} zoom={7} height={40} bind:this={mapTerrain} />
    <IslandCoordinates island={data.island} />
  </div>
  <div class="column">
    <IslandDescription island={data.island} />
  </div>
</div>
