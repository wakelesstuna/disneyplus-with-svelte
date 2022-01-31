<script context="module">
  export function load({ error, status }) {
    return {
      props: { message: error.message },
    };
  }
</script>

<script>
  export let message;
</script>

<div class="error">
  <h2>Ooops</h2>
  {#if message}
    <p>{message}</p>
  {:else}
    <p>404 Page Not Found</p>
  {/if}
</div>

<style>
  .error {
    text-align: center;
    margin-bottom: 60px;
  }
</style>
