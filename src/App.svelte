<script>
  import Tailwindcss from './Tailwindcss.svelte';
  import Router from 'svelte-spa-router'
  import SignUp from './routes/SignUp.svelte'
  import SignIn from './routes/SignIn.svelte'
  import ForgotPassword from './routes/ForgotPassword.svelte'
  import {userbaseStore, userStore, promiseStore} from './stores'
  const userbase = window.userbase
  window.userbase = null
  // stores
  $userbaseStore = userbase
  $userStore = null
  $promiseStore = userbase.init({appId: '1231870e-0438-4217-9005-8bea74e68100'})
          .then((session) => $userStore = session.user)

  function signout() {
    $promiseStore = $userbaseStore.signOut().then(() => $userStore = null)
  }
</script>

<Tailwindcss />

<div class="container flex flex-col justify-center items-center w-screen h-screen mx-auto">
  {#await $promiseStore.then(() => Promise.reject())}
  Loading..
  {:catch error}
  {#if error}
  <strong class="text-red-700 font-bold">ERROR! {error} </strong>
  {/if}
  {#if $userStore}
  Hello, {$userStore.username}!
  <button on:click={signout}>Logout</button>

  <section>
    <h1>
      <div id="logo">
        <picture>
          <img src="logo.png" alt="Taxi" width="200"/>
        </picture>
      </div>

      GoTaxi
    </h1>

    <h2 class="subtitle">Always on time</h2>

    <h2>
      Whether you’re visiting Paris and want to book a taxi from the train station <strong>to
      your hotel</strong>, need to get a cab from the city <strong>back home</strong> or are flying out from Paris
      airports and need an <strong>airport express taxi service</strong> in Paris to get you there as
      quickly as possible, you can rely on us.
    </h2>

    <p>Order your next ride !</p>

    <form>
      <label for="pickup">Pickup:</label>
      <input type="text"><br>

      <label for="destination">Destination:</label>
      <input type="text"><br>

      <label for="date">Date:</label>
      <input type="date" id="date" name="ridedate" value="2021-31-05" min="today" max="2021-12-31"><br>

      <label for="nbpassengers">Number of passengers:</label>
      <select id="nbpassengers" name="nbpassengers">
        <option value= "">Choose an option</option>
        <option value="1">1 passenger</option>
        <option value="2">2 passengers</option>
        <option value="3">3 passengers</option>
        <option value="4">4 passengers</option>
        <option value="5">5 passengers</option>
        <option value="6">6 passengers</option>
      </select><br>

      <input type="submit" value="Book">
    </form>
  {:else}
    <div id="logo">
      <picture>
        <img src="logo.png" alt="Taxi" width="200"/>
      </picture>
    </div>
  <h1>Welcome to the best VTC Taxi booking service !</h1>
  <Router routes={{
  '/': SignUp,
  '/signin': SignIn,
  '/forgotpassword': ForgotPassword
  }} />
  {/if}
  {/await}
</div>