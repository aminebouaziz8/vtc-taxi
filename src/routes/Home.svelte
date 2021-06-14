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
                <div class="form-check form-check-inline">
                    <button type="submit" class="btn btn-primary">Submit</button>
                </div>
            </form>
        </div>

    </section>
</div>