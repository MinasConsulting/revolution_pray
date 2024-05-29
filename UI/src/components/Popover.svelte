<!-- src/components/Popover.svelte -->
<script>
    export let isOpen = false;
    export let date = null;
    export let hourlyCoverage = [];
  
    function closePopover() {
      isOpen = false;
    }
  </script>
  
  <style>
    .popover {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background: white;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      padding: 2rem;
      z-index: 1000;
      max-width: 90%;
      width: 400px;
      text-align: center;
    }
  
    .backdrop {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: rgba(0, 0, 0, 0.5);
      z-index: 999;
    }
  </style>
  
  {#if isOpen && date}
    <div class="backdrop" on:click={closePopover}></div>
    <div class="popover">
      <h1>Prayer Coverage for {date.toDateString()}</h1>
      <div class="section">
        {#each hourlyCoverage as { hour, status }}
          <p>{hour} - {status}</p>
        {/each}
      </div>
      <button on:click={closePopover}>Close</button>
    </div>
  {/if}
  