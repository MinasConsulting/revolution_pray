<script>
    import SignUpPopover from './SignUpPopover.svelte';
  
    export let isOpen = false;
    export let date = null;
    export let hourlyCoverage = [];
  
    let isSignUpPopoverOpen = false;
    let selectedHour = '';
  
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
  
    function handleSignUp(hour) {
      selectedHour = hour;
      isSignUpPopoverOpen = true;
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
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
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
  
    .sign-up-button {
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      padding: 0.25rem 0.5rem;
    }
  
    .sign-up-button:hover {
      background-color: #0056b3;
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
            <button class="sign-up-button" on:click={() => handleSignUp(`${i}:00 - ${i + 1}:00`)}>Sign Up</button>
          </div>
        {/each}
      </div>
      <button on:click={closePopover}>Close</button>
    </div>
  {/if}
  
  <SignUpPopover {isSignUpPopoverOpen} hour={selectedHour} bind:isOpen={isSignUpPopoverOpen} />
  