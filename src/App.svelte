<script>


import Counter from "./lib/Counter.svelte";

// use this props with ... / spread
const props = {
  initCount: 0,
  maxCount: 5
}
</script>

<Counter {...props} other='not used yet'/>

<style>

</style>
