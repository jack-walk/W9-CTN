<script>
  import DatabaseHeader from '$lib/components/DatabaseHeader.svelte';
  import RankingList from '$lib/components/RankingList.svelte';
  import RankingCard from '$lib/components/RankingCard.svelte';

  let { data } = $props();

  let top20 = data.violations
    .sort((a, b) => a.rank - b.rank)
    .slice(0, 20);
</script>

<DatabaseHeader
  headline="Tainted Home Tracker"
  description="The Bronx buildings with the most lead paint violations"
  byline="NYCity News Service"
  date="March 2026"
/>

<RankingList title="Top 20 buildings by open violations">
  {#each top20 as building (building.id)}
    <RankingCard
      rank={building.rank}
      title={building.address}
      value={building.violationCount}
    />
  {/each}
</RankingList>