<!-- src/routes/login/+page.svelte -->
<script>
    import { goto } from '$app/navigation';
    import '../../app.css';
  
    let username = '';
    let password = '';
    const loginPass = import.meta.env.VITE_LOGIN_PASS;
  
    function handleLogin() {
      if (password === loginPass) {
        alert('Login successful!');
        goto('/home');
      } else {
        alert('Invalid password!');
      }
    }
  </script>
  
  <div class="login-container">
    <img alt="Revolution Church Logo" src="/flrc_images/Black Mark.png" />
    <h1>Login</h1>
    <input type="text" placeholder="Username" bind:value={username} />
    <input type="password" placeholder="Password" bind:value={password} />
    <button on:click={handleLogin}>Login</button>
  </div>
  