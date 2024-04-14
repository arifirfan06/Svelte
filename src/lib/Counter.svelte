<script>
  export let initCount
  // we can add initial value on props here
  export let maxCount = 12

  console.log($$props, $$restProps)

  let count = initCount
  const increment = () => {
    if (count === maxCount) return;
    count += 1
  }
</script>

<button on:click={increment}>
  count is {count}
</button>
