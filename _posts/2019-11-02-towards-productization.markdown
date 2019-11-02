---
layout: post
title:  "Towards Productization and Delivery of Machine Learning Solutions"
date:   2019-11-02 13:53:14 +0000
tags: productization
---

Machine learning, deep learning and artificial intelligence (these terms will be referred to as "learning paradigm" in the remainder of this essay) suffer from several issues that prevent them to be integrated into production effectively. This learning paradigm development assumes all the complexites that exist in traditional software development. However, due to its data-dependent nature, it has extra difficulties on its own. This essay will quickly go over some of those issues and provide guiding principles when adopting the learning paradigm into production systems.

An important thing is to pin-point the source of extra complexity of a learning paradigm system. In a traditional software system, the problem solution is directly constructed by the programmer, which makes it easier to control quality. In the learning paradigm, the problem solution is not directly created by the programmer. Instead, the programmer codes some procedure, from which the computer uses it to learn the problem solution from the data.

[graph]

This greatly complicates the pipeline, as the sanity of the solution now not only cannot be straightforwardly traced back to the errors (as in the case of traditional software development), but the sanity now be influenced by the procedure, and the data. This leads to several immediate problems as follows:

- _Data dependency_. The effectiveness of a solution is not only tied with the code, but also tied to the data that it is trained on. Hence, how the data is collected, labeled, cleaned, and accessed greatly influences how good the final solution can be. Tracking this information when the amount of data steady increases is a challenge. Also, without care, data dependency can become unstable, as slight changes in the data break the solutions.
- _Quickly evolving software stacks_. Software stacks are not mature and they are changing quickly. Moreover, different people will likely use different software stacks, uusally for good reasons. This makes designing a production system that principled enough to allows everything connects to each other, while tolerates some level of flexibility to allow innovation, hard.
- _Stochastic result_. Same model architecture, data, and training algorithm can result in different results. This makes it hard for debugging and troubleshooting.

In [1] and [2], the authors introduce some best practices and make know common problems and anti-patterns of learning paradigm development that are worth reading. This essay provides the guiding principles that should be adhered to when adopting learning paradigm in production.

**Data pipeline demonstrates how good the system is.**

Data pipline is one of the very central components of a learning paradigm system. It is not exaggeration to say that this system can break and make a machine learning product. Considerations should be made:
- How the data is organized?
- How the data is labele?
- How the data is cleaned?
- How the data is performed sanity check?
- How the data is versioned? Useful for reproducible ML components.
- What about data stages?

**Tolerable collection of full flows**

Such collection of full flows should be tolerable, in that it does not assume a specific software stack. As software stacks quickly evolving, this allows for flexible choice of software stack.

**Reproducible ML components**

A full flow might consist of multiple ML components. These components should have a central storage place and follow a predefined interface, along with inference and training code.


**Issues tracking**

This part is more of the human organization rather than technical organization, but the implication is the same important. At the heart, ML making is just problem solving. The final targets is to solve some specific problems. As ML is more complicated, there can be more problems arise during the course of solving the target problem. As a result, it is necessary to have a central place to track all issues, so that the team can be organized efficiently, and solution can be delivered to the clients satisfactorily.

**Continuous testing and monitoring system**

What to test and monitor to always know what happens.
