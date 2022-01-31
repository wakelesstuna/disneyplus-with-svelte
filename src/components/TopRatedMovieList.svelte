<script>
  import { onMount } from "svelte";
  import HorizontalList from "./HorizontalList.svelte";
  import { MOVIE_API_KEY } from "$lib/env";
  export let movies = [];

  onMount(async () => {
    const res = await fetch(
      `https://api.themoviedb.org/3/movie/top_rated?api_key=${MOVIE_API_KEY}&language=en-US&page=1`
    );
    const topRatedMovies = await res.json();

    console.log(topRatedMovies);
    movies = topRatedMovies.results;
  });
</script>

<div>
  <HorizontalList listId={"TopRated"} title={"Top Rated"} {movies} />
</div>
