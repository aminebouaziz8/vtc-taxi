<script>
  import { onMount } from "svelte";
  export let date;

  onMount(async () => {
    const res = await fetch("/api/date");
    const newDate = await res.text();
    date = newDate;
  });
</script>

<main>
  <div id="logo">
    <picture>
      <img src="../public/Logo.png" alt="Taxi" width="200"/>
    </picture>
  </div>
  <h1>Welcome to VTC Taxi</h1>
  <h2>
    Log in
  </h2>

  <br />

  <form action="/action_page.php" target="_self">
    <label for="email">Email:</label>
    <input type="text" id="email"><br>

    <label for="password">Password:</label>
    <input type="password" id="password"><br>


    <input type="submit" value="Log in">
  </form>

  <a href="./register">You don't have an account yet ? Register here</a>
  <h2>Today is:</h2>
  <p>{date ? date : 'Loading date...'}</p>
</main>
