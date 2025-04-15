# QCON London 2025 Recap

Here is what I am going to cover from the key takeaways and insights I picked from QCon London 2025:

## Table of content
- [Engineering Productivity and Developer Experience](#engineering-productivity-and-developer-experience)
- [Best Practices for Timeouts and Retries](#best-practices-for-timeouts-and-retries)
- [Building Event-Driven Architectures in Multi-Cloud](#building-distributed-event-driven-architectures-across-multi-cloud-boundaries)
- [How BBC handles Load Spikes](#how-bbc-handles-load-spikes)
- [Empowering Teams: Decentralizing Architectural Decision-Making](#empowering-teams-decentralizing-architectural-decision-making)
- [Interesting Quotes](#interesting-quotes)

## Engineering Productivity and Developer Experience

### Productivity is messing around and having fun

Holly Cummins(Red Hat) and Trisha Gee (Gradle) outlined the following:

- Developers need to stop being *the boiling frog* that does not know it has been boiled. Ask yourself the following questions:
    - Am I the frog?
    - Am I using stress as a proxy for productivity?
- Developer need to use and embrace what is called the `Dead Time`: *Do not just move efficiently from task to task*
    - Problem solving
    - Thinking
    - Staring into Space:
        - `S` stands for *Satisfaction and Well-being*
        - `P` stands for *Performance*
        - `A` stands for *Activity*
        - `C` stands for *Communication and Collaboration*
        - `E` stands for *Efficiency and Flow*
    - Play
    - Activities that can help our brain *DMN(Default Mode Network)*:
        - knitting
        - running
        - walking
        - showers
        - gardening
        - colouring
        - laundry
        - unloading the dishwasher
    - The following three combined together enhance productivity:
        - Happiness
        - Fun
        - Joy

### SpareBank 1 and SINTEF in Norway

- Avoid Personal Focus, Increase Team work:
  They observed during their research that developers and managers are mostly concerned about the following:
    - How is your task going?
    - Can someone approve my PR?
    - Have you figured out the critical error yet?
    - Are we on track with your task?
- Team Work and Flow reduce WIP
- Pair Programmming increase CD
- Create a good workspace for team work and pair programming

### AI Coding State of Play
From Birgitta Bockeler(Thoughtworks) research
- AI is here to stay, developers should not ignore it. AI can tremendously enhance productivity.
    - Are you and enthusiast?:
        - Don't say: *Why are you so slow when you have AI?*
        - Do Praise experimentation
    - Are you a skeptic?:
        - Don't say: *Why would you even think that could work?*
        - Do Praise experimentation
- Avoid Vibe coding by following these ways of working with Agents:
    - Plan First
    - Small sessions and concrete instructions
    - Make use memory like a readme file to remind the agent of tasks done and task ahead
    - Adhere to your organisation security policies

### Your Platform is not an Island
From Rachael Wonnacott - Fidelity International:

- DevEx matters, but is not everything
- Frame platform investments in terms of value to business stakeholders
- Design for integration within the broader software delivery lifecycle
- Treat your platform like a product, but not in isolation

## Best Practices for Timeouts and Retries

From Sam Newman's session on timeouts, retries, and idempotency in distributed systems:

- Set timeouts based on actual system behaviour:
    - Too short: you give up too early
    - Too long: you increase resource contention and affect system stability
- Do not ignore the rare cases when it takes more time than usual to process a request
    - Analyse them to find some insights about how your system works
- Timeouts are about prioritising system health over the success of a single request
- Always apply Jitter(randomisation) to delay for retries. This will help avoid retry storms that can cause a DDoS.

## Building Distributed Event-Driven Architectures Across Multi-Cloud Boundaries

Teena Idani from Microsoft shared practical techniques for tackling challenges that come with building resilient, low-latency and consistent system across cloud providers.

- To achieve low-latency:
    - Compress event data using Gzip, Brottli, Snappy or LZ4 to reduce network load
    - Use larger batches with higher batch timeouts to minimise network overhead
    - Set realistic timeouts -- cross cloud communication can take longer than expected
- To improve resilience:
    - Add circuit-breakers to avoid overloaded services
    - Use retries with exponential backoff and jitter to prevent retry storms
- To improve ordering and consistency for events
    - Send related events(e.g for the same user) to the same partition (e.g in Kafka)
    - Add revision number to events when producing them. It allows consumers to detect out-of-orders events
    - Use deferred event processing on consumers side if out-of-orders event arrives
    - Make consumers logic idempotent to handle duplicated events.

## How BBC handles Load Spikes

To meet huge traffic spikes demand during major events in the UK, BBC focuses heavily on:

- Elasticty
    - Caching at every layer - from CDN down to components close to the data store
    - Serverless architecture using AWS Lambda to easily scale during spikes
    - Pre-computation whenever possible. They compute results ahead of time and cache them
- Resilience
    - Use the hourglass architecture standardizing the following key mechanisms:
        - Caching
        - Circuit breakers
        - Feature Flags
- Security
    - Use threat modelling techniques to proactively brainstorm and identify vulnerabilities by asking the following questions:
        - What are we building?
        - What can go wrong?
        - What are we going to do about it?

## Empowering Teams: Decentralizing Architectural Decision-Making
Peter Hunter and Elena Stojmilova from Open GI shared their experience as architects on how to empower team to make architectural decisions:

- Any team can make any decision they need to:
    - As long as they have sought advice from all meaningfully affected parties and those with domain expertise
- They must record this advice publicly, alongside reasons for going against it if necessary
- Make use ADR to record decisions using this guide:
    - Context: clarify the why behind the decision
    - Options: Explore, weigh, and align with principles
    - Decision: Finalize and document your choice
    - Consequences: Review long-term effects
    - Feedback: Seek advice before or after deciding

## Interesting Quotes

```text
Any organisation that designs a system will produce a design whose structure is a copy of the organisation's communication structure
```

```text
Pleasure in the job puts perfection in the work
```

```text
Scaling is not about adding more servers. It is about designing for failure before it happens
```

```text
Good performance is like a strong dial tone - free from lag
```

```text
When designing a system, both functional and non-functional requirements must be considered. The same applies when hiring people
```
Lesson: It is easier to teach technical skills than to change someone personality.

```text
It is very hard to make something simple and hide all the complexity. It is much easier to expose all the complexity outside
```
Lesson: Building plaftorms are very complex, however we should have a simple and intuitive interface for the end user which is not an easy task.

```text
Consistency is a spectrum. It is not black and white
```
Lesson: Learn to adjust the consistency level based upon your use case.