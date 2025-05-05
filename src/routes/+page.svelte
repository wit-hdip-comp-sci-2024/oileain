<script lang="ts">
  import LeafletMap from '$lib/ui/LeafletMap.svelte';
  import { currentIsland, currentView } from '$lib/runes.svelte';
  import type { PageProps } from './$types';
  let { data }: PageProps = $props();
  currentIsland.value = null;
  currentView.value = 'Home';
</script>

<LeafletMap height={85} markerLayers={data.markerLayers} />
