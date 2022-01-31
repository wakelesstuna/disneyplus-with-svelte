<script>
  import FaAngleLeft from "svelte-icons/fa/FaAngleLeft.svelte";
  import FaAngleRight from "svelte-icons/fa/FaAngleRight.svelte";
  import MovieCard from "./MovieCard.svelte";
  export let movies;
  export let title = "Title";
  export let listId;
  let counter = 0;

  const swipeRight = () => {
    counter++;
    const list = document.querySelector(`#${listId}`);
    const carouselItems = document.querySelectorAll(`#${listId} li`);
    const size = carouselItems[0].clientWidth;
    const calc = size * 4;
    if (counter === 1) {
      const leftBtn = document.querySelector(`#left__btn__${listId}`);
      leftBtn.style.pointerEvents = "auto";
      leftBtn.style.opacity = 1;
    }
    if (counter === carouselItems.length / 4 - 1) {
      const rightBtn = document.querySelector(`#right__btn__${listId}`);
      rightBtn.style.pointerEvents = "none";
      rightBtn.style.opacity = 0;
    }
    list.style.transform = `translateX(-${calc * counter}px)`;
  };

  const swipeLeft = () => {
    counter--;
    const list = document.querySelector(`#${listId}`);
    const carouselItems = document.querySelectorAll(`#${listId} li`);
    const size = carouselItems[0].clientWidth;
    const calc = size * 4;
    if (counter === 0) {
      const leftBtn = document.querySelector(`#left__btn__${listId}`);
      leftBtn.style.pointerEvents = "none";
      leftBtn.style.opacity = 0;
    }
    if (counter < carouselItems.length / 4) {
      const rightBtn = document.querySelector(`#right__btn__${listId}`);
      rightBtn.style.pointerEvents = "auto";
      rightBtn.style.opacity = 1;
    }
    list.style.transform = `translateX(-${calc * counter}px)`;
  };
</script>

<div class="list__title"><h2>{title}</h2></div>
<div class="list__wrapper">
  <button
    id={`left__btn__${listId}`}
    class="scroll__btn left"
    on:click={swipeLeft}
    ><div class="icon icon__left">
      <FaAngleLeft />
    </div></button
  >
  <button
    id={`right__btn__${listId}`}
    class="scroll__btn right"
    on:click={swipeRight}
    ><div class="icon icon__right"><FaAngleRight /></div></button
  >
  <ul id={listId} class="list">
    {#each movies as movie (movie.id)}
      <li>
        <MovieCard {movie} />
      </li>
    {:else}
      <p>Loading...</p>
    {/each}
  </ul>
</div>

<style>
  .list__title {
    padding-left: 3em;
    background: transparent;
  }
  .list__wrapper {
    position: relative;
  }
  .scroll__btn {
    z-index: 1;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    cursor: pointer;
    min-height: 200px;
    min-width: 100px;
    background-color: transparent;
    border: none;
  }
  .scroll__btn:hover > .icon {
    color: #fff;
  }
  .left {
    left: 5px;
    pointer-events: none;
  }
  .right {
    right: 5px;
  }
  .icon {
    color: transparent;
    width: 45px;
    aspect-ratio: 1 / 1;
  }
  .icon__right {
    float: right;
  }
  .icon__left {
    float: left;
  }
  .list {
    display: flex;
    width: 100%;
    padding-left: 2em;
    padding-top: 1em;
    padding-bottom: 1em;
    list-style: none;
    transition: transform 250ms ease-in-out;
  }
</style>
