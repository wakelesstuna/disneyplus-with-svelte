<script context="module">
  export async function load({ fetch, params }) {
    const movieId = params.id;
    const res = await fetch(
      `https://api.themoviedb.org/3/movie/${movieId}?api_key=109250d4fd5ba8352a011e66296eee2c&language=en-US`
    );
    const movie = await res.json();
    if (res.ok) {
      console.log(movie);
      return {
        props: {
          movie,
        },
      };
    }

    return {
      status: res.status,
      error: new Error("Could not fetch users"),
    };
  }
</script>

<script>
  const calculateRuntime = (runtimeInMinutes) => {
    const time = new String(runtimeInMinutes / 60).split(".");
    const hour = time[0];
    const minutesToCalc = `0.${time[1]}`;
    const minutes = Math.floor(parseFloat(minutesToCalc) * 60);
    return `${hour} hr ${minutes} m`;
  };

  const extractYear = (date) => {
    return date.split("-")[0];
  };

  const formatGenres = (genres) => {
    let formatGenres = "";
    genres.forEach((e, i) => {
      if (genres.length - 1 === i) {
        formatGenres += e.name;
      } else {
        formatGenres += e.name + ", ";
      }
    });
    return formatGenres;
  };

  export let movie;
  export let movieRuntime = calculateRuntime(movie.runtime);
  export let releaseYear = extractYear(movie.release_date);
  export let genres = formatGenres(movie.genres);
</script>

<div class="movie__info__container">
  <div class="image__fade_left" />
  <div class="image__overlay" />
  <img
    class="backdrop__image"
    src={"https://image.tmdb.org/t/p/original/" + movie.backdrop_path}
    alt={movie.title}
  />

  <div class="movie__title__wrapper">
    <h2 class="movie__title">{movie.title}</h2>
  </div>
  <div class="year__wrapper">
    <p class="year">{releaseYear} • {movieRuntime}</p>
  </div>
  <div class="movie__genres_wrapper">
    <p class="movie__genre">{genres}</p>
  </div>
  <div class="movie__overview__wrapper">
    <p class="movie__overview">{movie.overview}</p>
  </div>
</div>

<style>
  .movie__info__container {
    color: #fff;
    width: 95%;
    margin: auto;
  }
  .image__fade_left {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: linear-gradient(90deg, #282c3b, transparent);
    z-index: -10;
  }
  .image__overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: rgba(0, 0, 0, 0.2);
    z-index: -5;
  }
  .backdrop__image {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    object-fit: cover;
    object-position: top;
    z-index: -15;
  }
  .movie__title__wrapper {
    padding-top: 1em;
    padding-bottom: 2em;
  }
  .movie__title {
    font-size: 3.5rem;
  }
  .movie__genres_wrapper {
    display: flex;
  }

  .movie__genre {
    font-size: 0.8rem;
    font-weight: 200;
  }

  .movie__overview__wrapper {
    width: 50%;
  }
  .movie__overview {
    margin-top: 1rem;
    font-size: 1.125rem;
  }
</style>
