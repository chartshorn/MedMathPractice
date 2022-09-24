<script>
  let revealed = false;
</script>

<span class="spoiler" class:revealed="{revealed===true}" on:click="{() => {revealed=true}}">
  <slot></slot>
</span>

<style>
  span {
    color: black;
    background-color: black;
    font-weight: bold;
    transition: 150ms;
    border-radius: 4px;
    display: inline-block;
    padding: 0 8px;
  }
  .spoiler.revealed {
    color: white;
  }
  span:hover {
    cursor:pointer;
  }
</style>