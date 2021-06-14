<script>
    import Button from '../components/Button.svelte'
    import Input from '../components/Input.svelte'
    import A from '../components/A.svelte'
    import {userbaseStore, userStore, promiseStore} from '../stores'
    import {push, pop, replace} from 'svelte-spa-router'
</script>

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