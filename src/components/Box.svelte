<style>
  .box {
    padding: 1em;
    width: var(--width, auto);
    height: var(--height, auto);
    max-width: 90%;
    border-radius: var(--border, 0.5em);
    box-shadow: 0 0 0.5em rgba(0, 0, 0, 0.1);
    margin: 2em;
    background-color: #fcfcfc;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
  }
</style>

<div class="box">
  <slot></slot>
</div>
