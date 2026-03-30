<script>
  let { data } = $props();

  console.log(`Loaded ${data.violations.length} buildings`);
  console.log("First record:", data.violations[0]);
</script>