<script>
  import Dog from "./Dog.svelte";
  import dogCountStore from "../stores/dogCount.js";
  const dogsToShow = 3;

  let dogCount;

  const unsubscribe = dogCountStore.subscribe(value => (dogCount = value));
</script>

<style>
  .header * {
    text-align: center;
  }
  .header > h1 {
    font-size: 60px;
    margin-bottom: 0;
  }
  .header > h2 {
    margin-top: 0;
    font-size: 20px;
    color: darkgrey;
  }

  .dogs {
    display: flex;
    justify-content: center;
  }

  .dogCount {
    text-align: center;
    margin: 20px;
  }
  .dogCount > span {
    font-size: 20px;
  }
</style>

<div class="header">
  <h1>Dogs</h1>
  <h2>Just dogs</h2>
  <p>click on the dogs to get new dogs</p>
</div>

<div class="dogs">
  {#each new Array(dogsToShow).fill(null) as dog}
    <Dog />
  {/each}
</div>

<div class="dogCount">
  <span>You've seen {dogCount} dogs!</span>
</div>
