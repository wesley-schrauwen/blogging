# About

This is a general how to on writing technical design docs. I've seen many ideas on the internet about how to write these
however it seems like good analogies or resources for graphs or even why graphs should be needed.

## Background

At a high level I struggled with this idea for a while. I originally spoke to a co-worker about writing something
as a sortive guide to creating these documents. I felt after doing some research and thinking more on the topic that
I could write a guide and think on it as on-going subject.

### What is a technical design doc

When ever I explain things to anyone i've always found it useful to do so in terms of simple analogies that non-technical 
people can even understand.

For writing technical design docs I found an online cooking recipe to be the most useful as an analogy. Delish (a cooking webiste) 
has some great examples and even food recipes.

What makes the cooking recipe's particularly good is their use of pictures, precise ingredients, cook times and a nice 
description of every step required for you to take the raw ingredients and eventually get the final product. Most importantly
however is that it is relatable. Many people have cooked or looked up a recipe at some point and undoubtedly understand the concept. 

Cooking recipes and technical design docs are much the same. 

- You need pictures, sequence diagrams, flow diagrams and class diagrams. People like to see the perfectly baked chicken and its ingredients.
- The ingredients you need, an exact list of changes required. API, Database, classes, business logic. 
- The quantities, the precise amount of pepper, salt and so on. What the exact API changes will be, where will they be consumed and produced.
- Concise descriptions of every step, goal and starting point. How the chicken goes from raw to the oven prepped and comes out baked.

### In summary

A technical design doc needs:

- Sequence, flow or class diagrams
- The precise changes made to the API, Database, Classes and Business Logic
- Concise descriptions

## Describing these changes

When it comes to cooking recipes we always expect to get quantities of the ingredients that we understand. A recipe
that explains the quantity of butter used in terms of cloves wouldn't make much sense. Similarly measuring the quantity
of flour used would be in grams or cups.

When it comes to describing the API, Database, Classes and Business Logic, Diagrams they each of have their own units of 
measurements that make sense in their own context.

### The units for each

API
- consumers
- producers
- routes / endpoints / method (RPC) calls
- error responses
- body responses

Database
- schema changes
- indexes
- multi step migrations
  - schema, data, seed

Classes and business logic
- methods
- interfaces
- parameters
- return types
- mutations

Diagrams
- actors / servers / class components

## Implementing

Whenever it comes to changing code the first point is to always understand the business problem being solved. Code is only
there to support the business in solving business problems. Every byte of code is a custom tool used to solve specific 
problems.

The second part is modelling that business problem into code.

There is a bit of a natural trade-off here. We want to solve the smallest business problem possible because this makes
modelling the code easier, however the smaller the business problem we solve, the easier it is to accidentally introduce
styles of coding that make addressing future business problems harder. There are ways to solve this but its beyond this 
document.

### New features

When creating new features its usually easiest to start with a sequence or flow diagram. Something which outlines 
the high level inputs, process and output.

To reuse the cooking a chicken analogy. 

_We start with a chicken, add ingredients, cook it, and then we have a chicken._

You could literally use that flow above to describe cooking any chicken. The first step of modelling code and understanding
the business problem can be just as broad. All it does is map the services being used to the business problem being solved.

#### Gathering outputs

The next step I like to follow is to understand the expected outputs. Do we want crispy chicken, some fruity tastes etc. 
Most people usually describe the outputs or the problem being solved at a high level quite well. Your job is through discussion
to search for any inconsistencies in the problem being solved and produce a very succinct and specific list of (requirements / expected outcomes).

#### Trimming the fat

_No you cant have a cooked chicken with laser robot arms_

This is usually the hard part, its healthy and yet stressful. Its the job of Product people to demand as much as they can get, its
the job of Engineering people to deliver reliably.

The process of gathering outputs and trimming the fat are usually repeated multiple times. Every discussion brings everyone
one step closer to agreement. Drafting and reviewing a specification usually happens in this phase. The more you do this 
process the easier it becomes.

#### Producing the spec

##### Diagrams

After going through the above enough times, the problem is well understood and its really just a case of presenting
the specification to your colleagues.

A sequence diagram or flow is usually perfect for starting off. Its high level enough that you dont need to answer any
difficult questions but still forces you to explain the consumers and producers of the feature as well as how we get
from raw chicken and ingredients to crispy chicken.

**Sequence** diagrams are perfect for explaining simple relationships from start to finish and the major points of contact

**Flow** diagrams help with modelling more complex relationships with minor and major points of contact.

**Class** diagrams help with explaining the individual methods, functions, parameters that are being created. These are usually
very detailed and probably not the most useful outside embedded or monolithic applications

For most purposes a sequence or flow diagram should more than suffice.

##### API Contracts / Database Specs

After producing the diagrams, figuring out the exact pieces which move over the network helps.

This is usually some standard API boilerplate, 200, 201, 202 or the usual error codes, 400, 401, 403, 404 or 500 along 
with the appropriate routes.

The most important piece here is to document the body of the request and response of every single producer -> consumer and 
keep the API layer simple. 

Keeping the API layer simple is very easy when there is a simple single producer -> single consumer.

When there are multiple producers -> single consumer or single producer -> multiple consumers then race conditions 
inevitably arise.

For databases this part usually involves migrations. Running migrations in as small a steps usually helps avoid headaches.

##### Business logic

The last part I focus on is the business logic. This part flows very naturally after the above is decided on.

##### Scaling, reliability, maintainability, extensibility, usability, security

_the ilities of architecture_

Designing Data Intensive applications gives a nice overview of the _ilities_ of software architecture

For most technical design docs each of these topics can be very complex. Analogies here in terms of cooking chicken
aren't entirely useful.

As a basic, maintainability would always include logging. 

Unless the design document specifically covers a problem of scaling, flakiness, security or extensibility its probably
better to not think too deeply on these topics in the document.