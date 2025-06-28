# About

Add some information about your project here.

# Installation

You can use the button below to install the pre-built firmware directly to your device via USB from the browser.

<div class="container">
    <div class="question-prompt">Select Smart Home Platform:</div>
    <div class="types">
        <label>
            <input type="radio" name="platform" value="HomeAssistant" />
            <div class="name">Home Assistant</div>
            <div class="description">Choose this for Home Assistant integration, with additional options for a Hardware Distance Sensor</div>
        </label>
    </div>

    <div id="homeAssistantOptions" class="hidden">
        <div class="question-prompt">Select Option:</div>
        <div class="types">
            <label>
                <input type="radio" name="haOption" value="Plain" />
                <div class="name">Plain</div>
                <div class="description">Choose this option if you don't have an I2C VL53L0X distance sensor.</div>
            </label>
            <label>
                <input type="radio" name="haOption" value="DistanceSensor" />
                <div class="name">Distance Sensor</div>
                <div class="description">Choose this option to enable an I2C VL53L0X distance sensor to measure the water level.</div>
            </label>
        </div>
    </div>

    <esp-web-install-button class="hidden"></esp-web-install-button>
</div>

<script
    type="module"
    src="https://unpkg.com/esp-web-tools@9/dist/web/install-button.js?module"
></script>

<script>
    document.querySelectorAll('input[name="platform"]').forEach(radio =>
        radio.addEventListener("change", function(event) {
            var selectedPlatform = event.target.value;
            var homeAssistantOptions = document.getElementById("homeAssistantOptions");
            var installButton = document.querySelector("esp-web-install-button");

            homeAssistantOptions.classList.add("hidden");
            installButton.classList.add("hidden");

            if (selectedPlatform === "HomeAssistant") {
                homeAssistantOptions.classList.remove("hidden");

                document.querySelectorAll('input[name="haOption"]').forEach(optionRadio =>
                    optionRadio.addEventListener("change", function() {
                        installButton.classList.remove("hidden");

                        if (this.value === "DistanceSensor") {
                            installButton.setAttribute("manifest", "firmware/hydro-ds.manifest.json");
                        } else if (this.value === "Plain") {
                            installButton.setAttribute("manifest", "firmware/hydro.manifest.json");
                        }
                    })
                );
            }
        })
    );
</script>
