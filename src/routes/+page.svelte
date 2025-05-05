<script lang="ts">
  import LeafletMap from '$lib/ui/LeafletMap.svelte';
  import { currentIsland } from '$lib/runes.svelte';
  import type { PageProps } from './$types';
  let { data }: PageProps = $props();
  currentIsland.value = null;
</script>

<LeafletMap height={85} markerLayers={data.markerLayers} />
