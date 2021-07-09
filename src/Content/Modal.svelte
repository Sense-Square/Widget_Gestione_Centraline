  
<script>
  export let showModal = false;
</script>

{#if showModal}
  <div class="backdrop" on:click|self>
    <div class="modal">
      <slot></slot>
    </div>
  </div>
{/if}

<style>
  .backdrop{
    width: 100%;
    height: 88%;
    position: absolute;
    background: rgba(0, 0, 0, 0.658);
    z-index: 9998!important;
  }
  .modal{
    padding: 10px;
    border-radius: 10px;
    max-width: 400px;
    height: 230px;
    margin: 10% auto;;
    text-align: center;
    background: #f6f6f6;
  }

</style>