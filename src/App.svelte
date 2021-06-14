<script>
  import Tailwindcss from './Tailwindcss.svelte';
  import Router from 'svelte-spa-router'
  import SignUp from './routes/SignUp.svelte'
  import SignIn from './routes/SignIn.svelte'
  import Profile from './routes/Profile.svelte'
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
<strong class="text-red-700 font-bold">ERROR! {error.message} </strong>
{/if}

{#if $userStore}
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">

<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <img src="/logo.png" alt="Taxi" width="40"/>
  <a class="navbar-brand" >GoTaxi</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item active">
        <a class="nav-link" href="#">Contact</a>
      </li>
    </ul>
    <form class="form-inline my-2 my-lg-0">
      <a class="nav-link" href="/profile">Hello, {$userStore.username}! </a>
      <button on:click={signout} class="btn btn-outline-danger my-2 my-sm-0" type="submit">Log out</button>
    </form>
  </div>
</nav>
<div class="container flex flex-col justify-center items-center w-screen h-screen mx-auto">


  <section>

    <div class="row justify-content-center">
      <div class="col-4">
        <h1 class="center subtitle" style="text-align: center;">Always on time !</h1>
      </div>
    </div>

      <div class="col-16">
        <h4 style="text-align: center">
          Whether you’re visiting Paris and want to book a taxi from the train station <strong>to
          your hotel</strong>, need to get a cab from the city <strong>back home</strong> or are flying out from Paris
          airports and need an <strong>airport express taxi service</strong> in Paris to get you there as
          quickly as possible, you can rely on us.
        </h4>
      </div>
    <p style="text-align: center">Order your next ride !</p>
    <div class="row justify-content-center">
      <form class="col-16">
        <div class="form-group">
          <label for="pickUp">PickUp</label>
          <input type="text" class="form-control" id="pickUp" placeholder="ex: Cergy">
        </div>
        <div class="form-group">
          <label for="destination">Destination</label>
          <input type="text" class="form-control" id="destination" placeholder="Ex: La Defense">
        </div>
        <div class="form-group">
          <label for="date">Date</label>
          <input type="date" id="date" class="form-control" value="2021-31-05" min="today" max="2021-12-31">
        </div>
        <div class="form-check form-check-inline">
          <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio1" value="option1">
          <label class="form-check-label" for="inlineRadio1">1 passenger</label>
        </div>
        <div class="form-check form-check-inline">
          <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio2" value="option2">
          <label class="form-check-label" for="inlineRadio2">2 passengers</label>
        </div>
        <div class="form-check form-check-inline">
          <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio3" value="option3">
          <label class="form-check-label" for="inlineRadio3">3 passengers</label>
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
      </form>
    </div>

</section>

</div>
<footer class="bg-light text-center text-lg-start">
  <div class="text-center p-3" style="background-color: rgba(0, 0, 0, 0.2);">
    © 2021 Copyright:
    <a class="text-dark" >VTC Taxi</a>
  </div>
</footer>
{:else}
<div class="container flex flex-col justify-center items-center w-screen h-screen mx-auto">
  <h1>Welcome to THE BEST WAY TO book a Taxi !</h1>
  <Router routes={{
  '/': SignUp,
  '/signin': SignIn,
  '/forgotpassword': ForgotPassword
  }} />
</div>
{/if}
{/await}