<img width="1435" alt="image" src="https://user-images.githubusercontent.com/75016496/143686961-60067c38-71b7-4981-9298-e17729d18372.png">

# Violet SmartSwitch Lite with Home Assistant

The [Violet smart switch](https://violet-ultra.co.uk/product/smartswitch-lite-uk-eu/), at time of writing, integrates with a Phillips Hue hub and provides a beautiful touch screen interface allowing you to activate hue scenes. That's great, but I wanted to use the light switch with my [Shelly DUO bulbs](https://shelly.cloud/products/shelly-duo-smart-home-automation-bulb/) and I already have [Home Assistant](https://www.home-assistant.io/) running on a RaspberryPi, so here's an explanation of how I got that working, in case you want to do the same!

The smart switch is expecting to talk to a Phillips Hue bridge on your network. The first thing I did was discover this great add-on for Home Assistant called Emulated Hue. It exposes an API to your network which the smart light switch will recognise as a Hue hub.

<img width="330" alt="image" src="https://user-images.githubusercontent.com/75016496/143687093-4ca38e30-9723-460d-abca-4e5c84f41214.png">

Having the Emulated Hue add-on installed allows you to use an app like Hue Essentials (or any similar app, but not the official Hue app,) to control all of the lights that are connected to your Home Assistant. Do go and have a read of the full details of that add-on:
https://github.com/hass-emulated-hue/core

That's great, but the smart switch is all about scenes. Using the method above, you have to define the Hue scenes yourself via an app before the smart switch can use those scenes - but of course Home Assistant already has all my scenes defined, I'd rather use those! Because of that, I've enhanced the standard Hue Emulator code, (which is the purpose of this repo here on GitHub,) so that the home assistant scenes are the ones being shown to the switch!

Now let's run through the setup:

#### 1. Add the repo to your add-on store in Home Assistant
The Hue Emulator is in a custom repo, so you'll first need to add that repo to your add-on store:

In Home Assistant, go to Supervisor > Add-on store > click the ellipses (3 dots thing in the top right)
Choose 'Repositories' in the drop down.
Paste the URL below into the 'Add' section and click the ADD button
- https://github.com/hass-emulated-hue/hassio-repo

#### 2. Install the DEV version of the Emulated Hue add-on
The dev version allows us to run a custom version of the code.

<img width="700" alt="image" src="https://user-images.githubusercontent.com/75016496/143686988-03bade7c-4244-4563-b52a-838ca238c47e.png">

#### 3. Point Emulated Hue to the custom code

On the 'Configuration' tab for Emulated HUE (dev) just paste the path to my version of the code <b>finopsfuntimes:core:master</b> and click save.
(You can of course just fork from my version of the code and use your own copy!)

<img width="500" alt="image" src="https://user-images.githubusercontent.com/75016496/143687298-f01f334f-62a8-41f0-8545-d7321dce8618.png">

#### 4. Start the add-on

On starting, the add-on first downloads the code from GitHub but go and keep an eye on the logs and make sure everything looks OK before moving over to the light switch!

#### 5. Add the integration on the light switch!

At this point you're back to just following the standard instructions for setting up the Violet smartswitch lite!

Some notes:
- When first connecting, there will be a notification in Home Assistant prompting you to enable pairing mode
- In the Phillips Hue world, you have rooms - in Home assistant we have areas. These concepts are the same.
- If your scenes in Home Assistant are not associated with an area, they will be found in the 'No area' room when setting up the switch.

(You might prefer to go and associate your scenes with relevant areas in HA before setting up the switch:)
<img width="300" alt="image" src="https://user-images.githubusercontent.com/75016496/143687283-9ebf62c9-fb1a-435b-bae2-17b7997f8f67.png">

