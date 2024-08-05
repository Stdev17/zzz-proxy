<script>
  export let src = "";
  export let char = "";
</script>

<style>
  .char {
    padding: 0;
    width: var(--width, auto);
    height: var(--height, auto);
    border: 1px solid black;
    margin: 0;
    display: flex;
  }
  .img {
    width: 100%;
    height: 100%;
    background-size: cover;
    background-position: center;
  }
</style>

<div class="char">
  <slot>
    <img src={src} class="img" alt={"A portrait of "+{char}} />
  </slot>
</div>
