<!-- src/routes/home/+page.svelte -->
<script>
    import { goto } from '$app/navigation';
    import '../../app.css';
  
    const today = new Date();
    const prayerCoverage = {
      // Example data; should be fetched from an API or data source
      '2024-05-01': 'low',
      '2024-05-02': 'medium',
      '2024-05-03': 'high'
    };
  
    function getCoverageClass(date) {
      const dateString = date.toISOString().split('T')[0];
      return prayerCoverage[dateString] ? `day-${prayerCoverage[dateString]}-coverage` : '';
    }
  
    function handleDateClick(date) {
      goto(`/calendar/${date.toISOString().split('T')[0]}`);
    }
  
    function generateCalendar() {
      const calendar = [];
      const firstDayOfMonth = new Date(today.getFullYear(), today.getMonth(), 1);
      const lastDayOfMonth = new Date(today.getFullYear(), today.getMonth() + 1, 0);
      const firstDayIndex = firstDayOfMonth.getDay();
      const lastDay = lastDayOfMonth.getDate();
  
      for (let i = 0; i < firstDayIndex; i++) {
        calendar.push(null);
      }
  
      for (let i = 1; i <= lastDay; i++) {
        const date = new Date(today.getFullYear(), today.getMonth(), i);
        calendar.push(date);
      }
  
      return calendar;
    }
  </script>
  
  <div class="container">
    <h1>Main Page</h1>
  
    <div class="section">
      <h2>Your Committed Prayer Hours</h2>
      <p>Mon 8:00 AM - 9:00 AM</p>
      <p>Wed 6:00 PM - 7:00 PM</p>
    </div>
  
    <div class="section">
      <h2>Prayer Guides</h2>
      <button>Access Prayer Guides</button>
    </div>
  
    <div class="section">
      <h2>Prayer Requests</h2>
      <button>Access Prayer Requests</button>
    </div>
  
    <div class="section">
      <h2>Prayer Calendar</h2>
      <div class="calendar">
        {#each generateCalendar() as date}
          {#if date}
            <div class="day {getCoverageClass(date)}" on:click={() => handleDateClick(date)}>
              {date.getDate()}
            </div>
          {:else}
            <div class="day"></div>
          {/if}
        {/each}
      </div>
    </div>
  </div>
  