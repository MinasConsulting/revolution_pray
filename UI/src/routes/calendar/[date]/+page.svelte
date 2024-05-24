<!-- src/routes/calendar/[date]/+page.svelte -->
<script>
  import { page } from '$app/stores';
  import { onMount } from 'svelte';
  import '../../../app.css';

  let date;
  let hourlyCoverage = [
    { hour: '00:00 - 01:00', status: 'available' },
    { hour: '01:00 - 02:00', status: 'covered' },
    // ... more hours
  ];

  $: currentPage = $page;
  $: {
    const dateParam = currentPage.params.date;
    date = new Date(dateParam);
    // Fetch hourly coverage for the date here
  }

  function formatHour(hour) {
    return `${hour}:00 - ${hour + 1}:00`;
  }
</script>

<div class="container">
  <h1>Prayer Coverage for {date.toDateString()}</h1>
  <div class="section">
    {#each hourlyCoverage as { hour, status }}
      <p>{hour} - {status}</p>
    {/each}
  </div>
</div>
