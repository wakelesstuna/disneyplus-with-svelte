<script>
  import { onMount } from "svelte";
  import IoMdHome from "svelte-icons/io/IoMdHome.svelte";
  import IoIosSearch from "svelte-icons/io/IoIosSearch.svelte";
  import IoIosAdd from "svelte-icons/io/IoIosAdd.svelte";
  import IoIosStar from "svelte-icons/io/IoIosStar.svelte";
  import IoMdFilm from "svelte-icons/io/IoMdFilm.svelte";
  import IoIosTv from "svelte-icons/io/IoIosTv.svelte";
  export let user = {
    username: "Oscar",
    avatar:
      "https://prod-ripcut-delivery.disney-plus.net/v1/variant/disney/C8C4B89DF57F29CA3D0FC0C0E10F77DD6C1C9D29C3B524A79241A3B1616B85E0/scale?width=96&format=png",
  };

  onMount(() => {
    const nav = document.querySelector("nav");
    document.addEventListener("scroll", function (e) {
      if (window.scrollY > 5) {
        console.log("In if");
        nav.style.backgroundColor = "#181b24";
      } else {
        nav.style.backgroundColor = "transparent";
      }
    });
  });
</script>

<nav>
  <div class="links__wrapper">
    <ul class="nav__list">
      <li>
        <a href="/" class="link__item"
          ><img
            class="logo"
            src="https://static-assets.bamgrid.com/product/disneyplus/images/logo.1a56f51c764022ee769c91d894d44326.svg"
            alt="logo"
          /></a
        >
      </li>
      <li>
        <a href="/" class="link__item "
          ><div><IoMdHome /></div>
          <p class="underline">Home</p>
        </a>
      </li>
      <li>
        <a href="/search" class="link__item"
          ><div><IoIosSearch /></div>
          <p class="underline">Search</p></a
        >
      </li>
      <li>
        <a href="/my-list" class="link__item"
          ><div><IoIosAdd /></div>
          <p class="underline">My List</p></a
        >
      </li>
      <li>
        <a href="/originals" class="link__item"
          ><div><IoIosStar /></div>
          <p class="underline">Originals</p></a
        >
      </li>
      <li>
        <a href="/movies" class="link__item"
          ><div><IoMdFilm /></div>
          <p class="underline">Movies</p></a
        >
      </li>
      <li>
        <a href="/series" class="link__item"
          ><div><IoIosTv /></div>
          <p class="underline">Series</p></a
        >
      </li>
    </ul>
  </div>
  <div class="user__wrapper">
    <div class="username">{user.username}</div>
    <div class="avatar__image">
      <img src={user.avatar} alt="profile" />
    </div>
  </div>
</nav>

<style>
  nav {
    width: 100%;
    display: flex;
    transition: all 250ms ease-in-out;
  }
  .links__wrapper {
    flex: 1;
  }
  .logo {
    width: 85px;
  }
  .nav__list {
    list-style: none;
    display: flex;
  }
  .link__item {
    position: relative;
    display: flex;
    align-items: center;
    padding: 1em 1.1em;
  }
  .link__item > div {
    width: 30px;
    aspect-ratio: 1;
  }
  .link__item > p {
    margin: 13px 0 13px 8px;
  }
  .user__wrapper {
    min-width: 10%;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
  }
  .username {
    margin: 0 1em;
    color: #fff;
    font-size: 1.125rem;
    font-weight: 500;
    letter-spacing: 1px;
  }
  .avatar__image > img {
    width: 50px;
    aspect-ratio: 1;
  }
  .underline {
    border-bottom: 3px solid transparent;
    transition: all 150ms ease-in;
  }
  .underline:hover {
    border-color: #fff;
  }
</style>
