---
title: "How I Made an Old House Warm Again with Home Assistant (Part 01) - The Idea and Hardware"
description: "In this first chapter, I tackle my parents' poorly insulated home using Home Assistant. From testing smart thermostatic valves to hacking cheap sensors, I share the hardware and ideas that set the stage for a smarter, cozier home."
date: "Jan 23 2025"
---

# How I Made an Old House Warm Again with Home Assistant (Part 01) - The Idea and Hardware

I've always wanted to start a blog and ramble about random hobbies I pick up because I find them cool on a Friday evening, or things I come across in my everyday life.

I guess the time has finally come.

I'm not a big writer, and you'll notice that right away, but hopefully, I'll improve over time.

I've been using Home Assistant for a little over a year now, and the main reason I started was that, while I'm still living at my parents' house for some reason (_cough_ saving money _cough_), the house is pretty cold and always has been.

The main issue, other than my parents being scared of the monthly bills and trying to keep the temperature as low as possible, is that in the past, they had the weird idea to put the thermostats on the coldest side of the house. Why? Well, it was probably because if the coldest side is warm, then every other place should be warm enough. But that's not the best approach. They likely didn't have a better or cheaper way to do it at the time, like having a thermostat per room, which would have involved a more complex and costly setup. Back then, my parents had little to no money, so they had to work with what they had.

So, can we do something about it now?

Well, it turns out that during the pandemic, I started building my own homelab, and I came to love everything about it. That's when I discovered this _cool af_ project called **Home Assistant**. It's open-source and can be hosted on our little servers right away.

Home Assistant gives us the ability to write automations, create scripts, build dashboards, and connect a wide variety of devices seamlessly.

I won't go into detail about all the possibilities Home Assistant has to offer just yet, but we'll discover them together as we go along.

The house currently has two main thermostats: one for the ground floor and one for the first floor.

The two thermostats work as dry relays, meaning when they request heat (because the room temperature falls below a certain setpoint), they close the contact, which turns on the pump responsible for that specific floor.

The two main relays for both pumps are also connected in a way that they tell the boiler to warm up the water whenever one of the two is on. I plan to replace the relays with a single Zigbee module, but I think I'll save that for the last chapter of this adventure since it's mostly about cleaning up the mess they made in that little electrical box.

So, let's see.. Every room has at least one radiator, so I guess there's no other way to control the temperature other than managing those somehow. That's where smart thermostatic valves come in.

Sure, we could simply turn on the heat for the entire floor and turn it off when all the rooms reach a certain temperature, but our house has another issue: bad thermal insulation (I know.. I don't know what to say). Because of this, some rooms get way colder than others based on many different factors.

I've tested different brands: the cheap and noisy Tuya ones, the reasonable but kinda useless Sonoff TRVZB, and the cool, silent, but kinda expensive Danfoss Ally valves. At one point, my setup became quite messy.

I didn't spend much time with the Tuya valves because I found them too noisy for a bedroom, so I only got one. The [Sonoff TRVZB valves](www.amazon.it/dp/B0CFXY26H1) are pretty and relatively cheap, but they didn't provide any way to adjust their aperture/closure at the time (though they recently pushed a firmware update that allows you to set those parameters but we'll talk about that later). That's where the [Danfoss Ally valves](www.amazon.it/dp/B08DRCVDG4) shine: they're quiet, have built-in PID control that seems to work well enough in my case without needing additional automations, and they just work. Sure, they're a bit expensive, but I was able to grab five brand-new ones for €25 each on Subito.it, and there seem to be quite a few other sellers offering them at similar prices.

I didn't like the idea of having to replace batteries, but they seem to last quite a while.

Now that we've figured out how to control each radiator, we have to find a way to get the temperature of each room. Well.. there isn't really any other way out other than having a single thermometer per room. And we have so many options in this case but it all comes down to budget and your Zigbee setup (I'll talk about why later).

Of course, I went with the "cheap" option (I'm joking but saving in this case is just too funny and cool) and grabbed a couple of Xiaomi LYWSD03MMC Bluetooth sensors off AliExpress for like €5 each.

Wait.. Bluetooth? Weren't we going with Zigbee?

Well, guess what? Those cheap Xiaomi sensors do support Zigbee under the hood, and some cool people built custom firmware for them to enable this protocol.

The only issue they have is that the custom firmware only makes them operate at +2dB to save battery, so you need to set up your Zigbee "mesh" network properly to ensure they're always relatively close to a repeater or your Zigbee router.

You can find a cool guide on how to convert them to Zigbee [here](https://smarthomescene.com/guides/convert-xiaomi-lywsd03mmc-from-bluetooth-to-zigbee/).

Another good option is the [SONOFF SNZB-02D](https://www.amazon.it/dp/B0BYZP8NK2). I've got two, and you won't have range issues with them, but they're quite expensive compared to the Xiaomi ones, as they go for around €16 on Amazon.

Okay, the idea seems good, and the hardware is ready as well.. Wait, how do we turn on the pump?

My setup for that is quite temporary right now, so I won't go into much detail, but I hacked a [SONOFF MINI R2 smart switch](www.amazon.it/dp/B08NBGQ6NC) to work as a dry relay switch. You have to open it up, cut some traces, and solder some stuff, so I won't suggest you do the same. It'll be replaced by a single Zigbee module later on, as described before.

I guess everything is ready to warm the house up now. We just have to automate and connect everything together somehow, but it's better if we talk about that in another blog post.

See ya!
