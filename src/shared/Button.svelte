<script>
  export let type = 'primary',
    flat = false,
    inverse = false;
</script>

<style>
  button {
    border: 0;
    cursor: pointer;
    border-radius: 5px;
    padding: 8px 12px;
    font-weight: bold;
    font-size: 0.9rem;
    box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.2);
  }

  .primary {
    background: #d91b42;
    color: white;
  }

  .secondary {
    background: #45c496;
    color: white;
  }

  .flat {
    box-shadow: none;
  }

  .primary.inverse {
    background: white;
    color: #d91b42;
    border: 1px solid #d91b42;
  }

  .secondary.inverse {
    background: white;
    color: #45c496;
    border: 1px solid #45c496;
  }
</style>

<button class={type} class:flat class:inverse on:click>
  <slot>
    <!-- optional fallback -->
  </slot>
</button>
