<script>
  import Roster from './Roster.svelte';

  let numRosters = 1;
</script>

<div class="buttons">
  <button on:click={() => numRosters = Math.max(1, numRosters - 1)}>⊖</button>
  <strong>{numRosters}</strong>
  <button on:click={() => numRosters++}>⊕</button>
</div>

{#each new Array(numRosters) as _, i (i)}
<div class="roster">
  <Roster />
</div>
{/each}

<style>
.buttons {
  margin-bottom: 2rem;
  padding: 1.5rem;
  border: 1px dotted black;
    display: flex;
    gap: 1.5rem;
    justify-content: center;
  }

.roster + .roster { margin-top: 4rem; padding-top: 2rem; border-top: 1px dotted black; }

@media print {
    .buttons {
      display: none;
    }

    .roster {
      break-after: page;
    }

    .roster + .roster {
      border-top: none;
      margin-top: 0;
      padding-top: 0;
    }
  }
</style>