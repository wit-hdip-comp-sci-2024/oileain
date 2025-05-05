<script lang="ts">
  import IslandCoordinates from '$lib/ui/IslandCoordinates.svelte';
  import IslandDescription from '$lib/ui/IslandDescription.svelte';
  import LeafletMap from '$lib/ui/LeafletMap.svelte';
  import type { PageProps } from './$types';
  let { data }: PageProps = $props();
  import { currentIsland } from '$lib/runes.svelte';

  currentIsland.value = data.island;
</script>

<div class="columns">
  <div class="column">
    <LeafletMap id="map-main" marker={data.marker} zoom={7} height={40} />
    <IslandCoordinates island={data.island} />
  </div>
  <div class="column">
    <IslandDescription island={data.island} />
  </div>
</div>
