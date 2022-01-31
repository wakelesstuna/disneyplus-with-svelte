<script>
  import MovieCard from "../../components/MovieCard.svelte";
  import { onMount } from "svelte";
  import { MOVIE_API_KEY } from "$lib/env";

  let searchQuery;
  export let searchResult = [];

  const checkKeyPress = (event) => {
    if (event.key === "Enter") {
      fetchSearch();
    }
  };

  const fetchSearch = async () => {
    const resp = await fetch(
      `https://api.themoviedb.org/3/search/movie?api_key=${MOVIE_API_KEY}&language=en-US&page=1&include_adult=false&query=${searchQuery}`
    );
    const data = await resp.json();
    searchResult = data.results;
  };

  onMount(async () => {
    const randomNumber = Math.floor(Math.random() * 10);
    const resp = await fetch(
      `https://api.themoviedb.org/3/discover/movie?api_key=${MOVIE_API_KEY}&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=${randomNumber}&with_watch_monetization_types=flatrate`
    );
    const data = await resp.json();
    searchResult = data.results;
  });
</script>

<div>
  <input
    class="search__input"
    placeholder="Search for tv show or movie"
    type="text"
    on:keydown={(e) => checkKeyPress(e)}
    bind:value={searchQuery}
  />
  <div class="discover__container">
    {#each searchResult as result}
      <MovieCard movie={result} />
    {:else}
      <p>No data found for {searchQuery}</p>
    {/each}
  </div>
</div>

<style>
  .search__input {
    outline: none;
    text-overflow: ellipsis;
    border: none;
    background: rgb(75, 78, 90);
    color: rgb(168, 169, 173);
    padding-left: calc(3.5vw + 2em);
    height: 100px;
    font-size: 2.6rem;
    width: 100vw;
  }
  .discover__container {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    max-width: 95%;
    margin: auto;
  }
</style>
