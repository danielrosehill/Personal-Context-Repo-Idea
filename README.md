# Personal Context Repository for Large Language Models (LLMs)

*By: Daniel Rosehill. 14-Dec-24*

The purpose of this repository is to provide a high-level conceptual outline of a system for enabling users to create, edit and modify a personal contextual repository. 

The purpose of the personal contextual repository is to provide an organized data source to improve and contextualize the inference of large language models. 

The contention underlying this system is that in a future in which consumers increasingly use a plurality of large language models for their daily work, coupling one's contextual data store to any one model is going to be increasingly untenable. Furthermore, it is argued that the very nature of personal contextual data argues strongly that consumers should remain the controllers of such a data repository and not any one external company. 

The question of how consumers can go about building and maintaining their own contextual data store is very much an unaddressed one. This document provides some thoughts about why this might be useful and suggests some initial path towards developing a proof-of-concept for this purpose.   Comments, pull requests and invitations to collaborate on experiments slash prototypes slash POCs are more than welcome (my email is in the sidebar).

## Overview
 
LLMs are incredibly powerful and useful tools, but whether they derive their knowledge from data they were exposed to during their training period, or through more modern and sophisticated techniques like RAG or API calls, their knowledge is primarily general in nature. 

Enriching LLMs through personal context about the user greatly increases their utility. 

Simple examples: 

- LLMs which have knowledge of their user's movie preferences can instantly provide more guided, targeted and relevant movie recommendations.  
- An LLM with simple contextual data about the user's professional life, such as their resume and career aspirations, can provide targeted recommendations for professional development opportunities, new jobs, etc (without needing to be explicitly instructed to do so).    
- An LLM which understands the user's computer hardware can instantly provide compatible recommendations for upgrades, etc. 

From a technical standpoint, contextual data can be exceedingly light, captured initially in simple JSON files and then vectorized. But this data, though "weighing" almost nothing in technical terms, can still yield outsized results in dramatically improving the quality of inference. 

Coupling the power of LLMs for reasoning with their increasingly multifaceted general knowledge and then layering onto that an understanding of the specificities of the user yields enormous value. When this works effectively (targeted prompting generating an output which draws upon both relevant data and personal context considered expertly by the LLM), LLMs become qualitatively different technologies than the search engines which preceded them as the favored means for information retrieval.

##  Where ChatGPT's implementation of memory failed and succeeded

In March 2024, OpenAI added a memory feature to ChatGPT. It has been met with mixed results from both expert commentators and ordinary users. The main deficiency of the memory module is that it is only capable of storing up to 1,400 words of memories in total. While the memory module has shown many how useful contextual data can be when used in LLM interactions, its utility, aAt the time of writing, is severely hampered by its very small size. 

## Contextual memory data should be a personal information store

Large language use is experiencing an explosion in popularity. The frenzied pace of development activity in models, coupled with dramatic changes in pricing such as those recently seen with OpenAI’s shifts, have led many to adopt a slightly more vendor agnostic posture, trying out different models, seeing what works,and just as commonly using different models for different applications. By trying to tailor their use of models to their different strengths, consumers can better test the waters of this fast moving scene. Among enthusiasts, use of open source and self-hostable LLMs is increasingly mainstream, popular and feasible, providing alternatives to using cloud large language models altogether. 

The increasingly fragmented state of the LLM market, however, poses an unsolved challenge for the question of user memory and context. 

It directly challenges the very premise that a memory or context module should necessarily be coupled with any one specific UI, or platform or model. In the current state of affairs, a user subscribing to both ChatGPT and Anthropic Claude may find that ChatGPT has learned about their occupation through ongoing interactions, but that Anthropic is naive when it comes to this fact. This creates a disjointed and confusing user experience.

From a data sovereignty standpoint too it can be argued that the very idea of vendors attempting to monopolize users contextual data is inherently problematic. 

While bureaucrats are happy to devise elaborate legislation imposing strict requirements on what companies do with very small pieces of personal information (|see: GDPR et al), when it comes to the often much more significant and sensitive information that users routinely commit to large language models, or which are derived by them from their interactions, nobody bats an eyee.

 This is particularly strange given the unique sensitivity of this data. Beyond containing personally identifiable information (PII), raising compliance responsibilities, it may also contain much more emotional and sensitive data like someone's life aspirations, challenges, etc.   A strong answer from the open source community could be precisely what's needed to instill in users that this data should not be freely up for grab.

## The idea: a personal context repository (self-managed / self-hosted / SaaS with safeguards)

Here is the central part of this idea and the argument underpinning it:

We're accustomed to having a cloud data storage pool in which we aggregate our information (consider Google Drive as an example). Many would argue that Google have proven themselves to be *reasonably* responsible custodians of the data that we routinely commit into their servers in this matter. Those who feel less rosy in their assessment can self host document management systems. But there remain a variety of approaches open to users who wish to gather and manage this pool of data. . 

Similarly, we could have a place where our contextual data is gathered and which we use to enhance the capabilities of whatever AI systems we are interacting with, *(but particularly large language models given their easy accessibility and the fact that they are particularly well-suited for this kind of information).* In certain types of generative AI work, a personal context RAG pipeline might not actually be advantageous at all - consider, for example, text to image generation tools. For these tools, user preferences could continue to be provided through the more simple and established mechanisms, like user settings or small snippets of preference text that the get injected to the models by mechanisms like text precedence. For tools like chatbot, centric LLMs however a  much more wide-reaching and robust bank of contextual data about the user could have far more significant benefits. 

## How a detailed personal context "repo" could be developed

The development of a personal context repository could be achieved through two means. It's important to point out that these are not mutually exclusive. Additionally, it might be possible for users to choose one or the other path depending on their level of comfort with external providers having access to their personal contextual repository. 

A more skeptical user could only provide read access to LLMs, for example, while someone who was more comfortable with the idea could provide both read and write access, allowing the LLMs access to the data (ie, read access) while allowing them to write back modifications or additions to the data storage. If access could be. controlled at a more granular level, as is increasingly becoming the standard in other applications, the write permission could be fine-grained so that only creating new documents was permitted, but editing existing context or deleting it were prohibited. 

Depending on how security controls were implemented and the user's preferences, one of the two following methods could be used for developing contextual data at scale and at pace:

The first is through deliberate context setting exercises. .

In this method, the user may interact with a specialised context setting AI tool which “interviews” them and then gathers common points of context into discrete documents.  For example, a large language model could interview the user in a sort of free ranging conversation about their current job and career aspirations. The transcript generated from this interview could then be used to generate specific contextual snippets each containing specific aspects of the data gathered. 

This method could be implemented through a simple question answer workflow.  The user might choose to have a totally free range interview with the LLM jumping between topics and "topping up" or updating existing contextual snippets. Or they might choose to have a more focused conversation, dialing down upon a specific topic with the intention of generating new pieces of context within that specific domain of life, for example, career aspirations or current health issues

The second path to building up a context repository could come from large language models feeding data back into this repository.  This process would mirror approximately the flow seen in ChatGPT (currently) in which users are not explicitly asked for their permission for data gathered in conversations to be written into the memory, rather, this happens as an autonomous background process during interactions.  This provides a more fluid way for the contextual information to be gathered and parsed. The only drawback is the size constraint seen in the chat GPT implementation Another limitation that a user who rarely touches upon topics and then suddenly decides to talk about them will find that the context for that particular subject is essentially totally bare. . 

Given the sensitivity of the information contained, granular and rigid write and read access controls would need to be instituted (much as users need to carefully review requests for integrations with their Google Drive).  

## The important of context being an evolving data pool

 It's important to point out that while some pieces of context are basically immutable (consider where a person was born) other pieces of personal context data are in a regular or periodic state of flux (consider, for example, whether a user is currently looking for a job).  At some points in their life this will be true and at other points this will be false. 
 
 To be both as accurate and useful as possible, therefore, a personal context library would need to be rewritten at intervals. These small adjustments to the context pool could be updated in a continuous and natural matter. During a conversation, a user might tell the large language model that he or she has just started a new job. If the model had previously noted that the user was job hunting the file could simply be updated with the LLM using logical inference to determine that the job hunt was no longer in progress  

## Paths to implementation & POC

In order to prove the concept, an experiment could be devised. The following components of the stock are envisioned and would be needed:

- For the deliberate context setting method to function. a frontend for managing, editing, adding personal context could be developed. This store could be writing data to a vector database on the back end. 

- A RAG pipeline could be developed running between the context repository database and a large language model. For feasibility testing, this could be an open source but capable model such as LLAMA 3.3 70 TB. 

- A series of evaluation prompts could be tested to benchmark the extent to which the model is utilizing the context available to it without needing to be explicitly instructed to do so by the user, something which cannot and should not be expected. For example, the user might ask the LLM for advice upon personal training they might undertake. The hoped-for response would be that the LLM guides its response through the vantage point of the context or about the user's career.  The failure criterion here would be the LLM, providing generalist career advice or asking them for data that was already in context these responses demonstrating either ignorance of the context repository's existence or failing to know when using it would be appropriate. 

## Use-Case

While much innovation is currently taking place in the realm of RAG for business use cases (for example pipelines providing internal CRM data into internal LLM tools), very little attention has been given to the question of how memory and context could be optimally handled for private users. Given that private use has been the major driving force of development in LLMs to date this in time might be seen as a mistake. At a minimum, it is a topic worthy of investigation and analysis.

The model proposed above necessitates careful attention to data management, but could spark an interest in the question of data sovereignty and federacy in the era of generative AI, which can only be expected to keep growing. 
