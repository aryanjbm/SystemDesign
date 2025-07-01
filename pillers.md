# A Framework for Thinking in System Design

When we build software, it's easy to get lost in the code. We focus on making features work. But what separates a simple program from a great, enduring system? The answer lies in moving beyond functionality and asking deeper questions about quality.

Every great system, from the simplest mobile app to the largest distributed service, is built on three pillars:

### Reliability: 
Does the system work correctly and consistently, even when faults occur? It's the promise that the system won't lose your data or give you wrong answers.

### Scalability: 
Can the system handle growth gracefully? As load increases (more users, more data, more traffic), does performance remain acceptable?

### Maintainability: 
How easily can engineers work on the system? Can new team members understand the code? Can we fix bugs and add features without breaking everything?

These pillars give us the language to describe a system's quality. But how do we apply them? We can use a simple, two-step thinking model for any design challenge.

## The Two-Step Framework for System Design
For any problem, start by asking two fundamental questions in order:

What should the system do? This is about defining the Functional Requirements. It's the list of features the user can interact with—the verbs of the system.

How well should it do it? This is about defining the Non-Functional Requirements. This is where we use the three pillars to set clear, measurable goals for the system's behavior.

This framework forces us to separate the "what" from the "how well," ensuring we build not just a working system, but a good one.

## Case Study: Applying the Framework to a To-Do List App
Let's apply this model to a deceptively simple application: a to-do list.

### Step 1: What Should It Do? (Functional Requirements)
First, we list the core features. A user must be able to:

* Create a new to-do item.

* Edit an existing item.

* Mark an item as complete.

* Delete an item.

This defines our scope. Now, we move to the crucial second step.

### Step 2: How Well Should It Do It? (The Three Pillars)
We'll use our pillars to set specific engineering targets.

#### Pillar 1: Reliability (The Promise)
What is the core promise of a to-do app? That it won't forget your tasks. If you add "Submit final project report" and your phone dies, that task must still be there when you reboot. This promise is called durability.

Reliability Requirement: The system must be durable. Once saved, data must not be lost.

#### Pillar 2: Scalability (Grace Under Pressure)
What happens when a user has 5,000 items in their list? The app can't take five seconds to load. We need to define "fast enough" with precise metrics.

Why 200ms? Human perception research shows that interactions that complete in around 100-200ms feel "instantaneous." Anything longer, and users start to perceive a delay. By targeting 200ms, we aim for an experience that feels fluid and responsive.

Why Percentiles? Simply measuring the average response time can be misleading. An average of 200ms could hide the fact that some users are waiting 2 full seconds while others get a 10ms response. We care about the consistent user experience. Using percentiles is much more powerful. A common metric is the 99th percentile (p99).

Scalability Requirement: The p99 latency for loading the list must be under 200 milliseconds, even with thousands of items.

This requirement translates to: "99 out of every 100 times a user opens the app, the list should load in under 200ms." This is a robust goal that ensures the vast majority of user interactions feel instantaneous, while still acknowledging that occasional, rare slowdowns can occur.

#### Pillar 3: Maintainability (A Gift to Your Future Self)
Software is never finished. In six months, we'll want to add due dates. A rigid, spreadsheet-like data structure (ITEM_ID, TEXT, IS_DONE) would make this a painful migration. A flexible, JSON-like structure makes it easy.

Maintainability Requirement: The system must use a flexible data schema to simplify adding new features.

## From Idea to Blueprint
By following this simple two-step framework, we transformed a vague idea ("a to-do app") into a clear engineering blueprint with specific, measurable goals.

This thinking model—defining functions, then applying the pillars of Reliability, Scalability, and Maintainability—is a universal tool. Whether you are designing a simple app or a system for millions of users, it provides the structure you need to build software that doesn't just work—it lasts.
