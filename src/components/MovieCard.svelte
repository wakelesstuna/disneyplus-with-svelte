<script>
  export let movie;
</script>

<div class="list__card">
  <a href={`/movie/${movie.id}`}>
    <div class="image__wrapper">
      <img
        class="blur"
        src={"https://image.tmdb.org/t/p/w500" + movie.backdrop_path}
        alt={movie.title}
      />
      <div class="content">{movie.title}</div>
    </div>
  </a>
</div>

<style>
  .list__card {
    overflow: hidden;
    width: 325px;
    height: 180px;
    margin: 1em 1em;
    border-radius: 5px;
    box-shadow: rgb(0 0 0 / 69%) 0px 26px 30px -10px,
      rgb(0 0 0 / 73%) 0px 16px 10px -10px;
    cursor: pointer;
    transition: all 300ms ease-in-out;
  }
  .image__wrapper {
    position: relative;
    overflow: hidden;
    width: 100%;
    height: 100%;
  }
  .image__wrapper > img {
    display: block;
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
  }
  .image__wrapper > .content {
    position: absolute;
    inset: 0;
    font-size: 2rem;
    padding: 1rem;
    color: rgb(46, 46, 46);
    background: rgba(255, 255, 255, 0.3);
    opacity: 0;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .image__wrapper:hover > .content {
    opacity: 1;
  }
  .image__wrapper > img,
  .image__wrapper > .content {
    transition: 200ms ease-in-out;
  }
  .image__wrapper:hover > img.blur {
    filter: blur(5px);
  }
  .list__card:hover {
    transform: scale(1.05);
    box-shadow: rgb(0 0 0 / 69%) 0px 26px 30px -10px,
      rgb(0 0 0 / 73%) 0px 16px 10px -10px;
  }
</style>
