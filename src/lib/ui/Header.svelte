<script lang="ts">
  import Icon from '@iconify/svelte';
</script>

<div class="columns is-vcentered">
  <div class="column is-two-thirds">
    <div class="box has-text-centered columns m-2 p-1">
      <div class="column is-2">
        <Icon icon="mdi:sun-compass" width="64" />
      </div>
      <div class="column">
        <div class="title">Oileain: islands of Ireland</div>
      </div>
    </div>
  </div>
  <div class="column">
    <div class="box has-text-centered columns m-2 p-1">
      <a href="/" class="column">
        <Icon icon="mdi:compass-rose" width="64" />
      </a>
      <a href="/explorer" class="column">
        <Icon icon="ph:compass-tool-duotone" width="64" />
      </a>
      <a href="/navigator/Great-Saltee-Island" class="column">
        <Icon icon="mdi:ruler-square-compass" width="64" />
      </a>
    </div>
  </div>
</div>
