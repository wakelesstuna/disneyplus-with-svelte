<script>
  import { onMount } from "svelte";
  import HorizontalList from "./HorizontalList.svelte";
  import { MOVIE_API_KEY } from "$lib/env";
  export let shows = [];

  onMount(async () => {
    const res = await fetch(
      `https://api.themoviedb.org/3/tv/top_rated?api_key=${MOVIE_API_KEY}&language=en-US&page=1`
    );
    const topRatedMovies = await res.json();

    shows = topRatedMovies.results.map((element) => {
      return {
        ...element,
        title: element.name,
      };
    });
  });
</script>

<div>
  <HorizontalList
    listId={"TopRatedTv"}
    title={"Top Rated Tv Shows"}
    movies={shows}
  />
</div>
