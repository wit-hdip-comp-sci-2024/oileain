<script lang="ts">
  import { oileainService } from '$lib/services/oileain-service';
  import type { IslandGroup } from '$lib/services/oileain-types';
  import Header from '$lib/ui/Header.svelte';
  import SideBar from '$lib/ui/SideBar.svelte';

  import { onMount } from 'svelte';

  let allCoasts: IslandGroup[] = [];
  onMount(async () => {
    allCoasts = await oileainService.getCoasts();
  });
</script>

<Header />
<div class="container">
  <div class="columns">
    <div class="column is-four-fifths">
      <slot />
    </div>
    <div class="column">
      <SideBar {allCoasts} />
    </div>
  </div>
</div>
