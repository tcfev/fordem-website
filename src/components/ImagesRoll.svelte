<script>
  import { onMount } from "svelte";
  const backend_url = import.meta.env.PUBLIC_BACK_API;

  let pictures = Array(11).fill({ url: "", id: 0, name: "" });

  onMount(async () => {
    pictures = (
      await fetch(`${backend_url}/index_pictures`).then((res) => res.json())
    )?.pictures;
  });
</script>

<section>
  {#each pictures as picture}
    <picture>
      {#if picture?.url}
        <img src={picture.url} width="200" height="200" alt={picture?.alt} />
      {/if}
    </picture>
  {/each}
</section>

<style>

  section {
    display: flex;
    flex-direction: row;
    justify-content: center;
    flex-wrap: wrap;
    gap: 10px;

    margin-top: 70px;
    height: 200px;
    width: 100vw;
    
    overflow-x: hidden;
    overflow-y: hidden;
    
  }

  img {
    min-width: 100%;
  }
  
  @media (max-width: 600px) {
    picture {
      min-width: 150px;
      height: 150px;
      margin-right: 5px;
    }
  }

  picture {
    background-color: #cdcdcd;
    height: 300px;
    width: 200px;
  }
</style>
