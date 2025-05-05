<script lang="ts">
  import { onMount } from "svelte";
  import { generateMarkerSpec } from "$lib/services/oileain-utils";
  import LeafletMap from "$lib/ui/LeafletMap.svelte";
  import IslandDescription from "$lib/ui/IslandDescription.svelte";
  import { currentIsland } from "$lib/runes.svelte";
  import type { MarkerSpec } from "$lib/services/markers";
  import type { PageProps } from "./$types";

  let { data }: PageProps = $props();

  let mapTerrain: LeafletMap;
  let mapSat: LeafletMap;
  let mapContext: LeafletMap;

  async function zoomTo(marker: MarkerSpec) {
    await mapTerrain?.addPopupMarkerAndZoom("selected", marker);
    await mapSat?.moveTo(marker.location, 14);
    await mapContext?.moveTo(marker.location, 10);
  }

  $effect(() => {
    const marker = generateMarkerSpec(data.island);
    currentIsland.value = data.island;
    mapTerrain?.addPopupMarkerAndZoom("selected", marker);
    mapSat?.moveTo(marker.location, 14);
    mapContext?.moveTo(marker.location, 10);
  });

  onMount(async () => {
    await zoomTo(generateMarkerSpec(data.island));
    currentIsland.value = data.island;
  });
</script>

<div class="columns">
  <div class="column">
    <LeafletMap id="terrain" height={40} bind:this={mapTerrain} zoom={14} />
  </div>
  <div class="column" style="height: 45vh; overflow-y: auto">
    <IslandDescription island={data.island} />
  </div>
</div>
<div class="columns">
  <div class="column">
    <LeafletMap id="sat" activeLayer={"Satellite"} height={40} bind:this={mapSat} zoom={14} />
  </div>
  <div class="column">
    <LeafletMap id="context" height={40} markerLayers={data.markerLayers} bind:this={mapContext} zoom={12} />
  </div>
</div>
