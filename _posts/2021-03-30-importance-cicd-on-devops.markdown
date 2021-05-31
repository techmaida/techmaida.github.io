---
layout: post
title:  "The importance of CI/CD on DevOps"
date:   2021-03-30 23:29:44
author: "João Paulo Maida"
tags: "DevOps, Unit tests, TDD"
---

Understand the importance of CI/CD on DevOps is one of the major goals to be achieved when a company decides to implement the truthful DevOps. But, why's that ?

Why do I have to understand the importance about this and why do I have the obligation to understand first what is CI/CD ? Of course, I am assuming that you know what DevOps is. But when I say "DevOps", I mean the truthful one. I am not referring to those cases where companies buy the most top existing tools on the market and think that all problems will be solved by these tools. I think, by my experience, that understand what DevOps really is the biggest challenge to be persued. That is the place where all the eyes should be and implement CI/CD comes next. So, this is my goal with this article, bring my point of view about what I believe to be DevOps, CI/CD and really understand what is the importance mentioned in article title.

So, what is DevOps ? In a really fast search on Google we can find the definition below:

"_DevOps is a set of practices that combines software development (Dev) and IT operations (Ops). It aims to shorten the systems development life cycle and provide continuous delivery with high software quality. DevOps is complementary with Agile software development; several DevOps aspects came from Agile methodology._"

But the point is: this definition doesn't help at all. Of course it doesn't help, it's to vague and of course it is vague, it's a cutout from Wikipedia. What were you expecting ? However, even if it is vague, it tells us some important things. DevOps wasn't born from one day to another. It has its foundations in others methodologies, as:
* Lean;
* Agile Manifesto;
* Agile Infrastructure and Velocity Moviment;
* Continuous Delivery (CD);
* Toyota Kata;

As you can see, it goes way further than a simple definition. Understand these methodologies is the key to understand DevOps and embrace it. I usually say that DevOps is a culture, but not only a culture, it is a lifestyle.

In a nutshell, Lean is focused in generating value to the final customer using the systemic way of thinking. It has a deep belief that demanded execution time of manufacture to convert raw material into finished products was the best quality and customer satisfaction predictor. It assumes shorter execution times were originated of small amounts of work. The Agile Manifesto, created in 2001, consists in a set of values and principles which oppose the heavy processes of software development. It has a important principle of delivering software frequently within a couple weeks or months.

The Agile Infrastructure and Velocity Moviment consists basically in a mobilization of important people to discuss the appliance of agiles principles on infrastructure instead of application source code, and how to create shared goals between Dev and Ops to deploy often.

Using the knowledge of building, testing and integrating continuously, Jez Humble and David Farley extended this whole concept to deliver continuously (CD) and create a new discipline in software engeneering. This practice defines a new implementation pipeline to ensure that source code and infrastructure are always implementable state.

Toyota Kata is a book written by Mike Rother that describes how he was surprised when he noticed that no companies of the automobile field achieved the same level of perfection that Toyota has and that's the target of this study. In this book he explains that each organization has its owns work routines, but to achieve perfection is necessary to create a structure focused on the daily practice of work improvement. And the truth is, you are already familiar with japanese practice of Kata.

Don't believe me !? See the picture below.

![Picture 1 - Daniel San and Mr Miyagi practicing Kata.](/assets/img/importance-cicd-on-devops/kata.png "Picture 1 - Daniel San and Mr Miyagi practicing Kata.")

Everytime that you watched the movie Karate Kid, specially this scene or the training on the beach, you were being presented to the practice of Kata. The whole idea of Kata is technique improvement. So how DevOps can be achievable if we still don't incorporate this practice, which is by the way, one of the DevOps foundations ?

That should be very easy to answer. Without feedbacks and continuous learning principles DevOps isn't achievable at all. These two practices united with the flow principle compose the three pillars of DevOps.

In a nutshell, the three principles make up everything that supports DevOps. The first one, flow principle, demands a fast and smooth workflow from Development teams to Operation teams in order to deliver results (value) to the customers. We optimize heading this global goal instead of local goals. We increase this flow making our work visible, reducing the workload size and work gap, and introducing quality, avoiding failures to pass to other work cores further. Accelerating the fluency through the technological value flow, we reduce the execution time demanded to serve requests from inside and outside customers, so we increase work quality while becoming more agile and able to step up against competition (Kim, Gene; Humble, Jez; Debois, Patrick; e Willis, John).

The value flow concept comes from Lean, once again Lean is here. In DevOps, value flow means the process demanded to convert a business hypothesis in a technological service which delivers valor to the final customer.

At this moment we face a concept derivated from Lean: **execution time** and **process time**. I don't need to mention how important this is because as you can see DevOps has a lot to do with Lean. So, expect to hear these terms again. Execution time is the time measured between the request creation by a customer and when it's fulfilled. The process time begins only when we start to work on this request (it omits the queue time, waiting to processed) (Kim, Gene; Humble, Jez; Debois, Patrick; e Willis, John). Remember this two concepts because they will be used along this article.

So, the flow principle's idea is: we need to accelerate our production making our work visible and introducing quality at the same time.

The second principle, feedback principle, defines what make possible the fast, constant and reciprocal feedback in all value flow stages. While the first principle works with concepts that make possible the fast value flow from left (to-do) to right (done), the second principle works in the opposite direction (right -> left) (Kim, Gene; Humble, Jez; Debois, Patrick; e Willis, John). And, you wonder: "why is that so important ?". Try the imagine the following situation: you work in toothpaste factory and some of the toothpaste products that are sold to final customers have a problem, the toothpaste box doesn't have a toothpaste tube. You got informed around this issue because one customer has posted on a social media his discontent and it has generated a lot of stress for you and your team. So, how can you prevent from situations like this ?

You start to question your colleagues and you found one who was suspecting that this could happen. You ask him: "Why didn't you tell me this earlier ?", he answered: "I didn't know how and the instructions that I receive are "keep going" and "don't stop the production chain".

As you can see in a simple example as that there isn't any feedback culture from the stages ahead of you. Your colleague, from the packaging department, was suspecting but his superiors didn't see value about this principle. So the main lesson here is: we make our work system safer creating a fast, frequent and high qualified information flow around our value flow and organization, which includes anticipated feedbacks loops (Kim, Gene; Humble, Jez; Debois, Patrick; e Willis, John).

You may wonder that situations like this doesn't happen in software development, and you're wrong. This happens and a lot ! You've propably passed by the same situation when the waterfall model was used, if you are that old (that's my case). When I started on software development this was the methodology used to build software. The waterfall model defined that first you collect all the requirements and following this order you project, implement, verify (test) and finally deploy. Just a few projects had success using this approach and the reason is obvious, you can spend years collecting and implementing but at the end see that doesn't satisfy your customer's needs. So, you spend more hours trying to adapt what you've built, consequence: more rework. That's why agile models as Scrum have conquered so much space, you get feedback earlier.

It's interesting to mention that feedback isn't just 'this is OK or not and can be improved', it isn't just a friendly advice. Feedback is also build new knowledge. DevOps leans on Toyota Kata using it's principle like **Andon's Cord** to build new knowledge. If I don't know how to do something or I'm facing some issue with some malformed or buggy component I pull a 'cord', in this case invisible, my tech leader gets informed and comes to my aid. After certain period of time if we can't solve it, all team is mobilized to help me to build a counter-measure. New knowledge is built and my issue doesn't spread to all team or anothers departments (Kim, Gene; Humble, Jez; Debois, Patrick; e Willis, John).

The last and third principle, continuous learning principle, is focused in a culture based on continuous experimentation and learning. Following this principle we can do experimentations in our software to anticipate risks and mistakes using scientific observations methods. This principle tries to answer one of the biggest question in software development: will our software work properly in a specific scenario ? Why try to discover that in a production environment if we can **experiment** that earlier ?

Our ultimate goal is to create a high trusted culture, learning with our successes and failures, identifying ideas that didn't work and reinforce those that worked. Besides, any local learnings are rapidly turned in global improvements, in a fashion that new techniques and practices can be used by the entire organization. Reserve time to work improvement daily is also important (remember what Kata is) so learnings can be accelerated (Kim, Gene; Humble, Jez; Debois, Patrick; e Willis, John).

Try to meditate about this last paragraph. We're talking about, maybe, introduce bugs to our software to see how it works and how our envinronment responds to this stimulus. Notice the amount of maturity to be at this stage. It isn't possible to start this all changing process/culture building and at first day say 'we're DevOps compliance'. It's almost a bad joke ! As I said in the beggining, it isn't only buy a bunch of tools, use Scrum or say that Ops team works together with Dev team, it is necessary to change people's minds, change the current process, the _status quo_, the system.

![Picture 2 - The classic conflict, before and after.](/assets/img/importance-cicd-on-devops/devops-explained.png "Picture 2 - The classic conflict, before and after.")

When we label DevOps just as a way to tear walls down like the one showed by the first frame of the picture above (most mainstreamed label), we are shortening the truthful power of DevOps and don't see the real challenge ahead us. You can't go from 0 to hero in one day, there is a journey to adopt those three principles and build maturity and confidence. Some of these principles will be hard to understand and apply in your scenario, it takes times to arrange. What we expect at the end is what frame 2 shows, integrated teams sharing knowledge, creating new knowledge and helping each other, the three principles.

Coming back to the very beggining of this article: why CI/CD is so important when we discuss DevOps ? I see CI/CD as an important player in this game because it puts on practice the three principles discussed. If I integrate my software with security and quality measures since day 1 using a pipeline, I am meeting the first principles requirements. If I can discover mistakes and learn with them earlier using unit tests associated with my pipeline, I collect the benefits of the second principle. If I experiment some new tech in my application, I can check how my entire pipeline behaved. Does this new tech breaks my compilation process ? How can I deploy faster ? How can I assure quality on my deploys ? These questions are just the tip of the iceberg about what CI/CD answers associated with DevOps.

It's important to understand that CI/CD represents just a facet in multifaceted prism, as we covered DevOps goes way further. This answers to another question done in the begging of this article.

You could wonder how difficult a CI/CD pipeline should be to leverage DevOps ? One that isn't difficult at all, the whole idea here is to make it simple.

por fim dizer como testes são importantes

### References
Kim, Gene; Humble, Jez; Debois, Patrick; e Willis, John; Manual de DevOps - Como obter agilidade confiabilidade e segurança em organizações tecnológicas; Alta Books Editora