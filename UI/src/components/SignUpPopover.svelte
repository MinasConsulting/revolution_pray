<script>
    export let isOpen = false;
    export let hour = '';
    
    function closePopover() {
      isOpen = false;
    }
  
    function handleOptionClick(option) {
      alert(`Signing up for ${hour} as ${option}`);
      // Implement sign-up logic here
      closePopover();
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
      z-index: 1001;
      max-width: 90%;
      width: 300px;
      text-align: center;
    }
  
    .backdrop {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: rgba(0, 0, 0, 0.5);
      z-index: 1000;
    }
  
    .button {
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      padding: 0.5rem 1rem;
      margin: 0.5rem;
    }
  
    .button:hover {
      background-color: #0056b3;
    }
  </style>
  
  {#if isOpen}
    <div class="backdrop" on:click={closePopover}></div>
    <div class="popover">
      <h1>Sign Up for {hour}</h1>
      <button class="button" on:click={() => handleOptionClick('One Time')}>One Time</button>
      <button class="button" on:click={() => handleOptionClick('Recurring')}>Recurring</button>
      <button class="button" on:click={closePopover}>Close</button>
    </div>
  {/if}
  