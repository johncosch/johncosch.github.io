---
layout: default
title: Elixir - Real Magic

![Elixir](https://www.google.com/url?sa=i&rct=j&q=&esrc=s&source=images&cd=&cad=rja&uact=8&ved=0ahUKEwjZ7dvXn8DLAhVDHB4KHcqmCZoQjRwIBw&url=https%3A%2F%2Fgithub.com%2Felixir-lang%2Felixir&psig=AFQjCNGNODf1Sw4Uezx8zHfqDH3RS0-gUA&ust=1458047322502818)
---
## Elixir - Real Magic
The definition of elixir is "a magical or medicinal potion." and that's pretty much exactly how I would describe the elixir programming language to other developers. Well...that's how it felt to me at least, like magic. Many of the features of Elixir sound too good to be true like it's incredible speed, efficient/simple concurrency, extreme reliability, hot code swapping, and powerful distribution. Of course, it's not really the Elixir language which facilitates this awesomeness. You can thank BEAM (the Erlang VM) for that, which Elixir runs on. I'm sure all of you are thinking, "Why hasn't Erlang taken over the world then if it can do all of this cool stuff too?". That's a great question because Erlang has been open source since 1998, and was used internally at Ericsson since 1986. I am certainly not an expert on the subject, but i'll try to summarize as best as I can.

### Elixir vs. Erlang
First let's start by taking a step back. Why is it that Elixir has all of this powerful functionality? It's because BEAM was built specifically for distributed systems. One of the most important ingredients of distributed systems is concurrency. In order to achieve this BEAM utilizes processes; no not the processes that your OS uses. You can think of these processes as super lightweight threads that interact through message passing. They're so lightweight, in fact, that even modest computers can run millions of these processes simultaneously. In most languages this level of concurrency is extremely error prone. That's because most OOP is all about state and with state comes inherent mutability. To get around this Erlang was built as a functional language. That means little to no state. Instead, functional programming utilizes concepts like pattern matching and recursion to transform data rather than simply reorganize it into a different state as with OOP. However there is a downside, it's very different than what most programmers are used to.  Which brings me back to my point of why Erlang hasn't been adopted as heavily as you might think for a language with so many great features. Do you remember when you learned OOP? You may not want to admit it, but i'm sure it was hard. Learning functional programming is just like that… hard. On top of that the Erlang syntax is very unfamiliar to many developers who first get started with it. I think it’s that enormous learning curve that scares programmers away from Erlang. Elixir aims to solve this issue. In my opinion many parts of Elixir's syntax serve to clarify functional programming paradigms, which helped me better understand what exactly was happening. An example of this is piping:

```
beer = bring_kettle_to_boil |>
       add_oats_and_barley |>
       boil_for_minutes(30) |>
       add_sugars |>
       boil_for_minutes(20) |>
       add_hops |>
       boil_for_minutes(20) |>
       ferment_for_weeks(2)

```

I’m sure you recognize this from unix, the code does a great job of describing exactly how you get from point a to b. Elixir also looks a lot like Ruby. Coming from the Ruby world I was feeling quite at home with Elixir, which made jumping right into the code a more pleasurable experience.

### Blowing Away the Competition
Although it's not easy to learn functional programming, the value add of using this approach is well worth it. Here are some key areas that elixir absolutely kills the competition.

#### Speed
It's FAST, requests are measured in microseconds. I've heard of ruby teams expecting 10x speed improvements.

#### Concurrency
Concurrency becomes significantly easier. Much less can go wrong when your not worried about state.

#### Reliability
AXD301 (Erlang’s flagship project) has achieved 99.9999999% reliability on BEAM. That means it's down less than a second a year. This comes from the the silo’d nature of processes and the OTP supervision tree - a concept which makes supervisor processes responsible for dealing with failing subprocesses.

#### Distribution
One of my favorite things about Elixir is the way it handles distribution. The VM itself allows you to arbitrarily spin up nodes across a network of servers and assign processes to them. Scaling up and down was literally built into the language.

### The Future

José Valim has stated numerous times that one of his primary motivations for building Elixir was because the so to speak "free lunch" was over, meaning that Moore's law would slow and developers would no longer be able to take advantage of speed increases from processing power enhancements at the same rate. This means that programmers would have to learn to use the hardware already in their machines more efficiently. Elixir fills in this need almost perfectly, allowing programmers to really utilize the cores in their machine. Here are some other trends in computing where elixir could have a substantial impact going forward.

#### Distributed Systems
Any large application today is distributed. Usually it takes some tying together a number of technologies to make it work. BEAM was built just for this, and should take care of most of the heavy lifting under the hood. Whats even better is that the architecture of elixir apps makes the currently dreaded task of scaling far simpler, and less error prone.

#### Real Time Communication
At the heart of real time communication is concurrency, and Elixir takes the crown in this area. Fields like Internet of Things require the speed, scalability, and uptime that only these functional languages can provide.

#### Automated Testing
This isn't exactly a new trend but i'm convinced it will be a nice selling point so i'll include it anyway. Since Elixir is based on transformation testing is far simpler and makes more sense intuitively. If I put it x it should be transformed to y.

#### Micro-Services
Elixir is made up of processes that are immutable and silo’d. Those processes are supervised by other processes which are supervised by applications which can be supervised by other applications. Each layer in the supervision tree can easily be broken out to be an application of its own. This pretty much fits exactly with the micro-service concept. José Valim explains it better himself here - [http://blog.plataformatec.com.br/2015/06/elixir-in-times-of-microservices/](http://blog.plataformatec.com.br/2015/06/elixir-in-times-of-microservices/)

### Conclusion
I'm still pretty new to Elixir, but as you can imagine i'm very excited about the future of this amazing technology. This was really a pretty scattered overview of the language, but i'm sure i'll be making some more specific posts about Elixir in the future.
