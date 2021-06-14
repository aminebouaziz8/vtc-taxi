<script>
import App from "../App.svelte";
import A from "../components/A.svelte";
import { userStore } from "../stores";

</script>
<div class="container flex flex-col justify-center items-center w-screen h-screen mx-auto">

    <section>

        <div class="row justify-content-center">
            <div class="col-4">
                <h1 class="center subtitle" style="text-align: center;">Contact us.</h1>
            </div>
        </div>

        <div class="col-16">
            <h4 style="text-align: center">
               A question? A feedback? Let us hear from you.
            </h4>
        </div>
        <div class="row justify-content-center">
            <form class="col-16">
                <div class="form-group">
                    <label for="pickUp">Email</label>
                    <input type="text" class="form-control" id="pickUp" placeholder="ex: Cergy">
                </div>
                <div class="form-group">
                    <label for="subject">Subject</label>
                    <textarea type="text" class="form-control" id="subject" placeholder="Write something..." style= "height:200px"></textarea>
                </div>
                <div class="form-check form-check-inline">
                    <button type="submit" class="btn btn-primary">Send</button>
                </div>
            </form>
        </div>

    </section>
</div>