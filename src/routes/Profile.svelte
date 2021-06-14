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
            <a class="nav-link" href="#">Hello, {$userStore.username}! </a>
            <button on:click={signout} class="btn btn-outline-danger my-2 my-sm-0" type="submit">Log out</button>
        </form>
    </div>
</nav>
<div class="container flex flex-col justify-center items-center w-screen h-screen mx-auto">


    <section>

        <div class="row justify-content-center">
            <div class="col-4">
                <h1 class="center subtitle" style="text-align: center;">Your Profile</h1>
            </div>
        </div>
        <div class="col-md-4">
        </div>
        <div class="col-md-4">
        </div>
        <div class="col-md-4">
            <h4 class="text-center"><strong></strong></h4>
            <hr>
            <div class="profile-card-4 text-center"><img src="http://envato.jayasankarkr.in/code/profile/assets/img/profile-4.jpg" class="img img-responsive">
                <div class="profile-content">
                    <div class="profile-name">{$userStore.username}
                        <p>@{$userStore.username}</p>
                    </div>
                    <div class="profile-description">Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor.</div>
                    <div class="row">
                        <div class="col-xs-4">
                            <div class="profile-overview">

                            </div>
                            <div class="col-xs-4">
                                <div class="profile-overview">
                                    <p>RIDES</p>
                                    <h4>XXX</h4>
                                </div>
                            </div>
                            <div class="col-xs-4">
                                <div class="profile-overview">
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</div>
<footer class="page-footer font-small blue">

    <!-- Copyright -->
    <div class="footer-copyright text-center py-3">© 2021 Copyright:
        <a> vtc-taxi.com</a>
    </div>
    <!-- Copyright -->

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
<footer class="page-footer font-small blue">

    <!-- Copyright -->
    <div class="footer-copyright text-center py-3">© 2021 Copyright:
        <a> vtc-taxi.com</a>
    </div>
    <!-- Copyright -->

</footer>
{/if}
{/await}
