<!-- src/components/Popover.svelte -->
<script>
    export let isOpen = false;
    export let date = null;
    export let hourlyCoverage = [];
  
    function closePopover() {
      isOpen = false;
    }
  
    function getHourClass(status) {
      switch (status) {
        case 'covered':
          return 'hour-covered';
        case 'available':
          return 'hour-available';
        default:
          return '';
      }
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
  
    .hour {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0.5rem;
      border-bottom: 1px solid #ddd;
    }
  
    .hour-covered {
      background-color: #d4edda;
    }
  
    .hour-available {
      background-color: #f8d7da;
    }
  
    .hour-time {
      font-weight: bold;
    }
  
    .hour-status {
      font-size: 0.9rem;
      color: #666;
    }
  
    .scrollable {
      max-height: 400px;
      overflow-y: auto;
      margin-top: 1rem;
      padding-right: 1rem;
    }
  </style>
  
  {#if isOpen && date}
    <div class="backdrop" on:click={closePopover}></div>
    <div class="popover">
      <h1>Prayer Coverage for {date.toDateString()}</h1>
      <div class="scrollable">
        {#each Array(24) as _, i}
          <div class="hour {getHourClass(hourlyCoverage[i]?.status)}">
            <span class="hour-time">{i}:00 - {i + 1}:00</span>
            <span class="hour-status">{hourlyCoverage[i]?.status || 'no coverage'}</span>
          </div>
        {/each}
      </div>
      <button on:click={closePopover}>Close</button>
    </div>
  {/if}
  