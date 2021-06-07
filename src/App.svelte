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
{#await $promiseStore.then(() => Promise.reject())}
Loading..
{:catch error}
{#if error}
<strong class="text-red-700 font-bold">ERROR! {error} </strong>
{/if}
{#if $userStore}
<header class="text-gray-600 body-font">
  <div class="container mx-auto flex flex-wrap p-5 flex-col md:flex-row items-center">
    <a class="flex title-font font-medium items-center text-gray-900 mb-4 md:mb-0">
      <svg xmlns="http://www.w3.org/2000/svg" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" class="w-10 h-10 text-white p-2 bg-yellow-500 rounded-full" viewBox="0 0 24 24">
        <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"></path>
      </svg>
      <span class="ml-3 text-xl">GoTaxi</span>
    </a>
    <nav class="md:ml-auto md:mr-auto flex flex-wrap items-center text-base justify-center">
      <a href="/home" class="mr-5 hover:text-gray-900">Home</a>
    </nav>
    <button  on:click={signout} class="inline-flex items-center bg-gray-100 border-0 py-1 px-3 focus:outline-none hover:bg-gray-200 rounded text-base mt-4 md:mt-0">Log out
      <svg fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" class="w-4 h-4 ml-1" viewBox="0 0 24 24">
        <path d="M5 12h14M12 5l7 7-7 7"></path>
      </svg>
    </button>
    <h3>Hello, {$userStore.username}!</h3>
  </div>
</header>
<div class="container flex flex-col justify-center items-center w-screen h-screen mx-auto">

  <section>
    <h1>
      <div class="logo">
        <picture>
          <img src="TaxiLogo.jpg" alt="Taxi" width="200"/>
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

    <form action="/action_page.php" method="get" class="homebook">
      <div class="homebook">
        <label for="pickup" >Pickup:</label>
        <input id="pickup" type="text">
      </div>

      <div class="homebook">
        <label for="destination">Destination:</label>
        <input id="destination" type="text">
      </div>

      <div class="homebook">
        <label for="date">Date:</label>
        <input type="date" id="date" name="ridedate" value="2021-31-05" min="today" max="2021-12-31">
      </div>

      <div class="homebook">
        <label for="nbpassengers">Number of passengers:</label>
        <select id="nbpassengers" name="nbpassengers">
          <option value= "">Choose an option</option>
          <option value="1">1 passenger</option>
          <option value="2">2 passengers</option>
          <option value="3">3 passengers</option>
          <option value="4">4 passengers</option>
          <option value="5">5 passengers</option>
          <option value="6">6 passengers</option>
        </select>
      </div>

      <div class = "submit">
        <a href="/login"><input type="submit" value="Book"></a>
      </div>
    </form>
  </section>
</div>
  <style>
    section {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      flex: 1;
    }
    h1 {
      width: 100%;
    }
    .logo {
      position: relative;
      height: 0;
      padding: 0 0 5% 0;
      margin-left: 20%;
    }
    label, input {
      display: table-cell;
      margin-bottom: 15px;
    }
    label {
      padding-right:100px;
    }
    form.homebook {
      display:table;
    }
    div.homebook {
      display: table-row;
    }
    div.submit {
      text-align: right;
      margin-top:30px;
      font-size: 20px;
    }
  </style>
  {:else}
  <div class="container flex flex-col justify-center items-center w-screen h-screen mx-auto">
      <div class="logo">
          <img src="logo.png" alt="Taxi" width="200"/>
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
