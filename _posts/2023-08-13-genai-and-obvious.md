---
layout: post
title: GenAI and Obvious-ish 
tags: llm ml gen-ai startup-scene 
---

For a tl;dr see the [Conclusion](#conclusion)

## Intro 

There are a few things that have felt "obvious" to me for the past a year and change about the GenAI space, especially LLMs. A lot of it was probably not obvious to folks in general, but via [working on chatbots before it resurged again](https://arxiv.org/pdf/2104.07567.pdf) and [kicking pretraining GPUs before ChatGPT for OPT175](https://github.com/facebookresearch/metaseq/blob/main/projects/OPT/chronicles/OPT175B_Logbook.pdf?fbclid=IwAR1Gz44159oYGepAF2dHu2tsow3IvQXkATjjC2Qyu-frwApGkj5AoNs0e3c) I got to see and think through a few things before everyone else did.  

In this, I go through some of the categories of clear areas of attack (["Obvious-ish next-ish stuff"](#obvious-ish-next-ish-stuff)), group them into the trends of what folks are building (["Observations"](#observations)), and provide my commentary on these and other promising potential areas (["My Opinions"](#my-opinions)).  

Interestingness to the reader is likely in the reverse order (with ["My Opinions"](#my-opinions) being the most). Former sections gives context and framing for latter ones though, so maybe worth a quick skim.   

## Obvious-ish next-ish stuff

The next steps of Large Language Model (LLM) development has been "obvious" for a bit. List of the semi-obvious things (**bold for tldr**):


1. Improve generation quality/accuracy by
   * ...**augmenting with tools**
      * external (vector) databases, search, code executors, memory, API calls in general (ex. plugins), etc, etc, etc
   * ...auto-manual-magical feeding generated (text, maybe regex'd) outputs back into itself (or a related smaller model) to check/verify/validate or to proceduralize things that one wants
      * ex. "let's think step by step", chaining (also related to tools), etc   
   * ...prompt-hacking, as the general superset of many of the things above but also to better control behavior
   * ...**RLHF**-y things
       * "reinforcement learning with human feedback" for those unfamiliar with the terminology. Think: getting humans to annotate the generated text from an LLM to see if it's good or not and then using that for training.
   * ...figure out some way to train with the above that works without too much catastrophic forgetting 
2. Go full multimodal or otherwise **improve base models**
   * By multimodal I mean multimodal in + multimodal out, sort of a la [Flamingo](https://arxiv.org/abs/2204.14198)'s interlaced text + image generation though also more than that (described more later)
   * Long context is the big recent innovation in base models; lots of stuff behind the scenes on data acquistion + cleaning; low-level architecture improvements that largely amount to "hand-optimizing transformer code for Nvidia GPUs" as well as training with lower-precision, etc   
3. **Build tooling** around the whole ecosystem
   * Ex. Monitoring, alerting, debuggability; model + prompt tracking + selection and general deployment logistics; evaluations  
   * Ex. Anything that could be described as "doing stuff with compute better"
      * Ex. inference/training efficiency, etc
      * Ex. GPU + cluster management 
4. Take anything and everything of the above and use it to **attack some specific product vertical** that other folks haven't spelunked in
 
<!---
 [^flamingo]: \<half-baked opinion\> ideally without tokenizing images as an information + soft-signal destroying hack for the "how do you deal with representing steps over time" problem, but that's an open research problem and definitely easier said than done. \</half-baked opinion\> Will be lots of use cases once promptable/feedback-able multimodal becomes that much more of a thing though. 
-->

  
Note that this ignores large swaths of the ML landscape, especially research side (ex. bias, safety, interpretability), related-but-not-exactly-ML finicky logistical infrastructure things (ex. compliance, data management, app hosting), etc.[^ignore]; [lots](https://techcrunch.com/2023/06/27/machine-learning-startup-investor-survey/) of [other](https://greylock.com/greymatter/the-new-new-moats/) folks [also](https://www.sequoiacap.com/article/llm-stack-perspective/) have [hot](https://a16z.com/2023/06/20/emerging-architectures-for-llm-applications/) takes.

[^ignore]:  There's definitely a nonzero bias towards the things that I'm intellectually interested-in (mostly reasoning + performance improvements...) that define how the grouping here is done. 


## Observations 

From hanging out in areas with the LLM hype:
* most folks don't touch [#2 pre-training] unless they're at [one](https://openai.com/) [of](https://www.anthropic.com/) [the](https://www.deepmind.com/) [known](https://ai.meta.com/) [well-funded](https://techcrunch.com/2023/05/31/character-ai-the-a16z-backed-chatbot-startup-tops-1-7m-installs-in-first-week/) [incumbents](https://techcrunch.com/2023/06/26/databricks-picks-up-mosaicml-an-openai-competitor-for-1-3b/) 
* most are doing some combination of [#1 quality improvement techniques] and [#3 building tooling] for the purposes of [#4 attacking a specific product vertical]
    * ...with very, very high variances in competency
    * ...especially with regards to understanding model limitations [^hallucination]
* and a smaller (but non-insignificant) portion of folks are doing [#3 building tooling] outright
    * ...oftentimes using a "picks + shovels in the gold rush" reference 
    * ...or some "but hey X is hard to use!" to talk about their specific value add, where X — or oftentimes, another system that's already built a platform around X — may be incentivized to build out the specific piece of tooling themselves. 

[^hallucination]: Cause one thing anyone that plays with these models realize is that these things still hallucinate up the wazoo. The more clever folks on the product side figure out use cases that work well within the limitation (ex. use cases where it's easy to check the answer, for brainstorming/creativity, areas where existing accuracy rates are far worse, etc); I've had far too many conversations where that hasn't been the case though. 


## My Opinions 

### On base model folks

I hear (not many, but a few whispers-in-the-wind) of folks trying to raise to build a LLM base model; my guess is it's *almost certainly too late now, especially cause the top-performers have long been accounted for*. Not to say that a new player couldn't come in and sweep everything else up, but with GPU knife wars, limited product mindshare, and the general crowdedness of the space... 

(I've got some other hot takes but they're not useful to share here; "oh sweet summer child" prolly summarizes the hottest of these takes though. :stuck_out_tongue_winking_eye:) 



 In a lot of ways, base model training *necessarily* requires more people: 
* It's *not* just the models but also all sorts of infra, safety/bias/alignment testing, etc, etc
* You also need folks for a product if you need to bootstrap for *more* $$

To this end, I imagine culture and care-in-setting-organizational-relationships is going be the high order factor in the ceilings of the different companies. Given the high \$\$\$\$\$ of funding, I imagine it'll take a few years (2-3?) to see the first real "death" of any of the well-funded pre-training startups. 


### On "tools around models" folks

Most of the smaller, newer players will: 
   * be acquired as offerings for the medium-large players 
   * bootstrap quick enough to *become* a medium-large player 
   * die  

Framed in another way: **Building picks and shovels during a gold rush is great, but what happens if the other person's getting traction for their Mining Tools Supercenter?**  

(I'm not an expert on B2B so not going to comment on medium-large folks much but I imagine the general properties of software infra + tooling apply.)

### On the "product vertical" folks

The same dynamics of vertical-specific consultancies will apply
   * ...just as it has for every other tech boom (ML, web, or otherwise)
   * ...cept it'll be that much harder for these sorts of players to turn generic cause those players (base model API platforms) are already there[^generic] 

[^generic]: by "turning generic" I mean something a la [snowboarding shop → ecommerce platform](https://en.wikipedia.org/wiki/Shopify#2006:_Founding)  


Most of the things in [#1 quality improvement techniques] of [the obvious-ish stuff](#obvious-ish-next-ish-stuff) isn't *that* hard to build. It's not trivial, but it's hard in an *infrastructure* way (ex. writing regexes, making API calls), not a *research ML* way (ex. needing to know deep mathematics, needing to keep up with large swaths of literature). You can get by with a bunch of medium-level engineers kludging things together as long as it doesn't devolve to spaghetti; we're still quite a few years out from the next sort of "generational-wow" leap anyway.

To this end, I think the moats for these product companies (assuming a sufficiently technical team) will be in sales, relationships, and reputation — technology will be a part of it, but only in-so far as to keep parity with what is offered on the market.  

There are lots of folks bearish on "LLM API wrapper companies" — I'm not so bearish as to think that *none* of them will survive, but I am *as skeptical of technical non-domain experts that have picked an area without prior experience* as I am of *insufficiently technical domain experts*.  

### On the topic of "generational-wow" leaps

My guess is that, even with all the RL/RLHF work, steadily tacked on prompts-among-prompts, and API-call-among-API-call systems, *we're still a few years out from a system where the reasoning capabilities of an LLM is generalized in an AGI-ish sort of way*. While chasing after generalized reasoning has a lot of promising directions, there's still a lot of "throw researchers at things and see what happens" to it, and it'll be hard to predict when that will settle. 

To that end, **I think the next big "PR hit" wave is gonna come from full(er) multimodal-in, multimodal-out models**. Ie, something where you give the model a physics problem with a diagram and it thinks step-by-step (both in text and in images) of how to solve it.

Or, given how [Google's Gemini is being lead by the folks that did the Atari game projects](https://www.wired.com/story/google-deepmind-demis-hassabis-chatgpt/) — something where it's *trained on multimodal screen-recordings of interactions on a computer, can be prompted with a task, and generates output videos of what it should look like to do said task, complete with annotations about where to click and what to type in*.  [^primer]

[^primer]: Or you know. Something where you put in the script/video of the entirety of [Primer](https://en.wikipedia.org/wiki/Primer_(film)) and have it make an understandable [movie narrative chart](https://xkcd.com/657/). Though, that might be beyond the scope of even the strongest of models. :stuck_out_tongue_winking_eye: 

Since the demos of this will be conceptually newer, it'll be trying to squeeze out the 80 in the ["80-20 rule"](https://en.wikipedia.org/wiki/Pareto_principle); to that end while there's still research risk for multimodal, it's also more 'finite' since the quality bar to beat is lower. Also while multimodal is more compute to train than language-only, this is the same sort of do-or-die scaling question these labs have already had to tackle. (Plus, the good labs are running out of raw text-only tokens to train on anyway.) 

Presuming the standard "release a model with an API platform" happens, this 'fuller multimodal API' will increase the ease of combining of sound/text/image[^modalities]. This opens up the potential for new "hit" experiences in ways that merely incrementally improving text performance wouldn't.  

It's probably too early to build any ideas anticipating this (unless one somehow gets early access to the APIs...) but that's maybe my hot take for "what would I keep an eye out on if I wanted to be ahead on things coming down the line".  


[^modalities]: Note that I've been intentionally vague about specifying modalities here (which is a very relevant and very hard problem if you're actually someone trying to *train* these models and also important if you want to *use* them). Also about how you represent time steps and the different "channels" of the modalities. That said, I do think I'm largely implying the normal-human-modalities of text, image, sound. The more esoteric ones can prolly be downstream fine-tuned anyway. 

## Conclusion

There's a lot of fast moving happening in the machine learning space around GenAI. However, despite the degree of real innovation, it's not clear to me (as someone that was in it early) if it is quite as 'easily ripe' from a company founding perspective as some of the hype might suggest. 

In summary: 
   1.  *There's a lot of good work happening in LLMs right now, but the finite number of ways to go means the space is crowded with folks largely gravitating towards the same sets of things.* 
   2.  *The next 'usable PR hit' will be more powerful forms of multimodal but it might be risky to act on it now without clearer idea of API, technical constraints, etc*. 


Anyway, thanks for reading! This has all been marinating in my head for a good little while, so hopefully some of y'all get some value from me externalizing the perspective.  

(Contact info is in the sidebar; will post links to threaded convos if I come across any.)  

