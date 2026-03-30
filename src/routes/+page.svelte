<script>
  import DatabaseHeader from '$lib/components/DatabaseHeader.svelte';
  import RankingList from '$lib/components/RankingList.svelte';
  import RankingCard from '$lib/components/RankingCard.svelte';
  import SearchInput from '$lib/components/SearchInput.svelte';

  let { data } = $props();

  let top20 = data.violations
    .sort((a, b) => a.rank - b.rank)
    .slice(0, 20);

  let search = $state('');

  let filtered = $derived(
    data.violations
      .filter(b => b.address.toLowerCase().includes(search.toLowerCase()))
      .sort((a, b) => a.rank - b.rank)
      .slice(0, 20)
  );
</script>

<DatabaseHeader
  headline="Tainted Home Tracker"
  description="The Bronx buildings with the most lead paint violations"
  byline="NYCity News Service"
  date="March 2026"
>
  <SearchInput bind:value={search} placeholder="Search by address..." />
</DatabaseHeader>

<div class="container">
  <RankingList title={search ? `Showing top ${filtered.length} results` : 'Top 20 buildings by open violations'}>
    {#each filtered as building (building.id)}
      <RankingCard
        rank={building.rank}
        title={building.address}
        value={building.violationCount}
      />
    {/each}
  </RankingList>
</div>

<style>
  .container {
    max-width: var(--max-width-wide);
    margin: 0 auto;
  }
</style>