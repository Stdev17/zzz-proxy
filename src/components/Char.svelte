<script lang="ts">
  export let src;
  export let name;
  export let showModal: boolean;

</script>

<style>
  .char {
    margin: var(--margin, 0.5em);
    width: var(--width, auto);
    height: var(--height, auto);
    border: 1px solid black;
    display: flex;
  }
  .img {
    width: 100%;
    height: 100%;
    background-size: cover;
    background-position: center;
  }
  button {
    background: none;
    border: none;
    padding: 0;
    cursor: pointer;
    outline: none;
  }
</style>

<div class="char">
  <slot>
    <button on:click={() => showModal = !showModal}>
      <img src={src} class="img" alt={`A portrait of ${name}`} />
    </button>
  </slot>
</div>
