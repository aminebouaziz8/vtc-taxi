<script>
  import Tailwindcss from './Tailwindcss.svelte';
  import Router from 'svelte-spa-router'
  import {link} from 'svelte-spa-router'
  import {push, pop, replace} from 'svelte-spa-router'
  import SignUp from './routes/SignUp.svelte'
  import SignIn from './routes/SignIn.svelte'
  import Profile from './routes/Profile.svelte'
  import ForgotPassword from './routes/ForgotPassword.svelte'
  import Home from './routes/Home.svelte'
  import Contact from './routes/Contact.svelte'
  import {userbaseStore, userStore, promiseStore} from './stores'

  const routes = {
    // Exact path
    '/': Home,
    '/signup': SignUp,
    '/signin': SignIn,
    '/forgotpassword': ForgotPassword,
    '/profile': Profile,
    '/contact': Contact 
  }
  const userbase = window.userbase
  window.userbase = null
  // stores
  $userbaseStore = userbase
  $userStore = null
  $promiseStore = userbase.init({appId: '1231870e-0438-4217-9005-8bea74e68100'})
          .then((session) => $userStore = session.user)
  function signout() {
    $promiseStore = $userbaseStore.signOut().then(() => $userStore = null);
    push('/signin');
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
        <a class="nav-link" href="/" use:link>Home <span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item active">
        <a class="nav-link" href="/contact" use:link>Contact</a>
      </li>
    </ul>
  
    <form class="form-inline my-2 my-lg-0">
      <a class="nav-link" href="/profile" use:link>Hello, {$userStore.username}! </a>
      <button on:click={signout} class="btn btn-outline-danger my-2 my-sm-0" type="submit">Log out</button>
    </form>
  </div>
</nav>
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
<Router {routes}/>

<footer class="bg-light text-center text-lg-start">
  <div class="text-center p-3" style="background-color: rgba(0, 0, 0, 0.2);">
    © 2021 Copyright:
    <a class="text-dark" >VTC Taxi</a>
  </div>
</footer>