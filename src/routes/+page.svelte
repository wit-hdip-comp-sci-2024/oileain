<script lang="ts">
  import LeafletMap from "$lib/ui/LeafletMap.svelte";
  import type { PageProps } from "./$types";
  let { data }: PageProps = $props();
</script>

<LeafletMap height={85} markerLayers={data.markerLayers} />
