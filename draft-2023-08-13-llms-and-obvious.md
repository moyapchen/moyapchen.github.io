---
layout: post
title: Generative AI and the "obvious"
tags: llm ml gen-ai startup-scene 
---

## Obvious-ish next-ish stuff

The next steps of LLM development has been "obvious" for a good solid while[^year]. List of the semi-obvious things (**bold for tldr**):

1. Improve gen quality/accuracy[^hallucination] by
   * ...**augmenting with tools**
      * external (vector) databases, search, code executors, memory, API calls in general (ex. plugins), etc, etc, etc
   * ...auto-manual-magical feeding generated (text, maybe regex'd) outputs back into itself (or a related smaller model) to check/verify/validate or to proceduralize things that one wants
      * ex. "let's think step by step", chaining (also related to tools), etc   
   * ...prompt-hacking, as the general superset of many of the things above but also to better control behavior
   * ...**RLHF**[^rlhf]-y things
   * ...figure out some way to train with the above that works without too much catastrophic forgetting 
2. Go full multimodal or otherwise **improve base models**
   * By multimodal I mean multimodal in + multimodal out, sort of a la Flamingo[^flamingo] though also more than that
   * Long context is the big recent innovation in base models; lots of stuff behind the scenes on data acquistion + cleaning; low-level architecture improvements that largely amount to "hand-optimizing transformer code for Nvidia GPUs"[^end] 
3. **Build tooling** around the whole ecosystem
   * Ex. Monitoring, alerting, debuggability; model + prompt tracking + selection and general deployment logistics; evaluations  
   * Ex. Anything that could be described as "doing stuff with compute better"
      * Ex. inference/training efficiency, etc
      * Ex. GPU + cluster management 
4. Take anything and everything of the above and use it to **attack some specific product vertical** that other folks haven't spelunked in
 
[^year]: Least a year and change, if not longer. Maybe not obvious to folks in general, but I was already [doing chatbots before it was cool](https://arxiv.org/pdf/2104.07567.pdf) and [been kicking LLM GPUs before ChatGPT](https://github.com/facebookresearch/metaseq/blob/main/projects/OPT/chronicles/OPT175B_Logbook.pdf?fbclid=IwAR1Gz44159oYGepAF2dHu2tsow3IvQXkATjjC2Qyu-frwApGkj5AoNs0e3c) so obvious from my vantage point.  

[^hallucination]: Cause one thing anyone that plays with these models realize is that these things still hallucinate up the wazoo. The more clever folks on the product side figure out use cases that work well within the limitation (ex. use cases where it's easy to check the answer, for brainstorming/creativity, areas where existing accuracy rates are far worse, etc). 

[^rlhf]: ...which may prove to ("reinforcement learning with human feedback" for those unfamiliar with the terminology. Think: getting humans to annotate the generated text from an LLM to see if it's good or not and then using that for training/prompting.)

[^flamingo]: \<soapbox\> ideally without tokenizing images as an information + soft-signal destroying hack for the "how do you deal with representing steps over time" problem, but that's an open research problem and definitely easier said than done. \</soapbox\> Will be lots of use cases once promptable/feedback-able multimodal becomes that much more of a thing though. 

[^end]: Though, short of major model architecture changes, it does seem like we might be hitting the limits of the juice worth squeezing there (ie getting close to some theoretical limits worth spending time on) though I don't follow that area tooo closely so maybe I'm off.  

   
Note ignoring large swaths of the ML landscape[^ignore]; [lots](https://techcrunch.com/2023/06/27/machine-learning-startup-investor-survey/) of [other](https://greylock.com/greymatter/the-new-new-moats/) folks [also](https://www.sequoiacap.com/article/llm-stack-perspective/) have [hot](https://a16z.com/2023/06/20/emerging-architectures-for-llm-applications/) takes.

[^ignore]: especially research side (ex. bias, safety, interpretability), related-but-not-exactly-ML finicky logistical infrastructure things (ex. compliance, data management, app hosting), and prolly some other stuff

## Observations 

From hanging out in areas with the LLM hype[^hype]:
* most folks don't touch #2 unless they're at [one](https://openai.com/) [of](https://www.anthropic.com/) [the](https://www.deepmind.com/) [known](https://ai.meta.com/) [well-funded](https://techcrunch.com/2023/05/31/character-ai-the-a16z-backed-chatbot-startup-tops-1-7m-installs-in-first-week/) [incumbents](https://techcrunch.com/2023/06/26/databricks-picks-up-mosaicml-an-openai-competitor-for-1-3b/) with 
* most doing some combination of #1 and #3 for the purposes of #4
    * ...with very, very high variances in competency
    * ...especially with regards to model limitations + quality [^hallucination]
* and a smaller (but non-insignificant) portion of folks are doing #3 outright
    * ...oftentimes using a "picks + shovels in the gold rush" reference or some "but hey X is hard to use!"[^framework] to talk about their specific value add.  


[^framework]: where X is a framework oftentimes with questionable adoption but has lots of mindshare, though oftentimes also something where a larger player in #3 or #2 might have a vested interest in building out themselves. 

[^hype]: Ie, random events in SF. There's some folks trying to make some very specific branding be a thing and I appreciate the very public social calendar, but I cannnnnnot bring myself to use that. 

## My thoughts

Base model training folks I generally respect. Or at least, the ones that'll likely survive[^survive]. 

Of the "tools around models" folks, the smaller players will: 
   * be acquired as features for the medium-large folks
   * bootstrap quick enough to become a medium-large player
   * die (but potentially not a slow death) 

Of the "product vertical" folks, the same dynamics of vertical-specific consultancies will apply
   * ...just as it has for every other tech boom (ML, web, or otherwise)
   * ...cept it'll be that much harder for these sorts of players to turn generic cause those players (base model API platforms) are already there 
        * by "turning generic" I mean something a la [snowboarding shop → ecommerce platform](https://en.wikipedia.org/wiki/Shopify#2006:_Founding)  

I'm not so bearish on LLM API wrapper companies to think that none of them will survive but I do think there are a lot of verticals that are already crowded. 

[^survive]: Too big too fail, early and competent, and already executed on an exit strategy being the "survival" criteria here. I've got hot takes on the rest that maybe aren't useful to share though there are some "sweet summer children" floating about. Might take 3-10 years to play out and yes lots of things *could* change, but I imagine cultural-and-organizational inertia (since base model things *necessarily* needs more people) is gonna be the high order factor.  


