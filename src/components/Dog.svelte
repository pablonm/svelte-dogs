<script>
  import { onMount } from "svelte";
  import dogCountStore from "../stores/dogCount.js";

  let loading = false;
  let dog;

  const incrementDogCount = () => dogCountStore.update(n => n + 1);

  const fetchDog = async () => {
    loading = true;
    const res = await fetch(`https://dog.ceo/api/breeds/image/random`);
    dog = (await res.json()).message;
    loading = false;
    incrementDogCount();
  };

  onMount(fetchDog);
</script>

<style>
  .dog {
    border: 1px solid black;
    margin: 10px;
    overflow: hidden;
    width: 300px;
    height: 200px;
    text-align: center;
    background: black;
    cursor: pointer;
  }

  .dog > img {
    max-height: 100%;
    max-width: 100%;
  }

  .loading {
    height: 100%;
    text-align: center;
    transform: scale(0.5);
    animation: 1s loading ease-out;
    filter: invert(100%);
  }

  @keyframes loading {
    from {
      transform: scale(0.5);
      opacity: 1;
    }
    to {
      transform: scale(0.7);
      opacity: 0.5;
    }
  }
</style>

<div class="dog" on:click={fetchDog}>
  {#if loading}
    <img class="loading" src="../assets/img/loading.gif" alt="loading" />
  {:else}
    <img src={dog} alt="dog picture" />
  {/if}
</div>
