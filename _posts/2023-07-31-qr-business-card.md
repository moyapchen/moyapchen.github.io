---
layout: post
title: QR code page
tags: meta creative art
---

I made myself a design for a business card today. 

Update Aug 1, 2023: Figured I'd move the write-up here, since there's a good chance I might keep iterating on this in the future and don't wanna spam the qr code page. 

## QR image generation

The QR codes were generated quick and hackishly with one of the out-of-the-box QR code + image prompt generators[^hacks]. In particular, [this thread](https://www.reddit.com/r/StableDiffusion/comments/14enj7a/a_generator_for_stable_diffusion_qr_codes_enter_a/) lead me to [this site](https://qrcodemonster.art/), though I tried a few different QR image generators. See [this directory]({{ '/public/qr_writeup/' | relative_url }}) for some examples. 

[^hacks]: Cause while I *could* get a model to run locally and tweek things a la [this write-up](https://antfu.me/posts/ai-qrcode), I didn't actually want to spend that much time doing this.


Here's a sample of some of the images I liked more[^city], from maybe an hour or two of prompting:

[^city]: As you may be able to tell, I had the idea of "futuristic city" for a good number of these. 

![QR image]({{ '/public/qr_writeup/hf_controlnet/image(3).png' | relative_url }}){: width="50%"}
![QR image]({{ '/public/qr_writeup/other_generator/qr.png' | relative_url }}){: width="50%"}
![QR image]({{ '/public/qr_writeup/monster/mountain_city.jpg' | relative_url }}){: width="50%"}
![QR image]({{ '/public/qr_writeup/hf_controlnet/image(2).png' | relative_url }}){: width="50%"}
![QR image]({{ '/public/qr_writeup/hf_controlnet/image(5).png' | relative_url }}){: width="50%"}

At one point, I decided to try one of the example prompts shown on the [QR Code Monster](https://qrcodemonster.art/) page. The output frankly looked way cooler than any of the prompts I had written.  
![QR image]({{ '/public/qr_writeup/monster/exact_prompt_copy.jpg' | relative_url }}){: width="50%"}

Being wary of the color palatte potentially not printing well (and also the difficuly of integrating such a complex background texture into a cohesive business card, especially cause I didn't feel like running an in-painting model), I played around with replacing the "orange" and "teal" in the original prompt until I eventually settled on the simple "black" and "white". 

![QR image used]({{ '/public/qr_writeup/monster/used_qr.jpg' | relative_url }}){: width="50%"}

Final prompt: 
```
a holistic drawing of (pc cooling:1.2) (printed circuitboard:0.2), (stunning, highly detailed, 8k, ornate, intricate, cinematic, dehazed, atmospheric:0.7), splash art, white, (black:0.3), (by Jeremy Mann, by John Constable, by El Greco:0.7), (acrylic paint:0.4), (by Zdzislaw Beksinski:0.4), (by Victo Ngai and John Romita Jr:0.8)
``` 

## Business Card Creation

Bit of tweaking in GIMP later[^gimp] (including generating another image with the same prompt to use as the background) and we get the business card that hopefully (unless you came from the blog) lead you here.[^doxx]

![GIMP screen of business card]({{ '/public/qr_writeup/gimp_qr.png' | relative_url }})

Since it seemed reasonable enough, I used [Vista Print](https://www.vistaprint.com/business-cards) to physically print the cards. For those curious, that site charges ~$25 on top of the cost of the card if you want to ship faster (~1 week) and $9 for the default cheap option of ~2 weeks.   


[^gimp]: Oh the joys of being cheap while funemploymed. :P 
[^doxx]: Middle bit here purposefully hidden to not doxx myself.

## Update (roughly an hour after making this)

I think I've realized the simpler answer here was probably to do QR art on the back side of a business card (letting it take up whatever space it needs), then have clean lines/text on the front. 

Ah well, done is better the enemy of perfect, and there'll always be more chances to print business cards. :P 



