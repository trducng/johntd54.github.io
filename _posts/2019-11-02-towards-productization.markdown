---
layout: post
title: "Towards Production and Delivery of Machine Learning Solutions"
date: 2019-11-02 13:53:14 +0000
tags: production
---

Machine learning (ML) solutions suffer from several issues that prevent them to be integrated into production effectively. This learning paradigm development assumes all the complexities that exist in traditional software development. However, due to its data-dependent nature, it has extra difficulties of its own. This essay quickly goes over some of those issues and suggests several guiding principles when adopting the learning paradigm into production systems.

First, it is important to pin-point the source of extra complexity of ML development compared to traditional software development. In traditional software development, the problem solution is directly constructed by the programmers, which makes it easier to control quality. In the learning paradigm, the problem solution is not directly created by the programmer. Instead, the programmer codes some procedure, from which the computer uses it to learn the problem solution in a probabilistic manner from the data.

This greatly complicates the situation, as the solution cannot be explicitly expressed in code, but indirectly described by the procedure code and the training data. This leads to several immediate problems as follows:

- _Data dependency_. How the data is collected, labeled, cleaned, and accessed greatly influences how good the final solution can be. Tracking this information with a continuously changing data source is a challenge. Moreover, without care, data dependency can become unstable, as slight changes in the data break the solutions.
- _Stochastic result_. Same model architecture, data, and training algorithm can result in different results. This makes it hard for debugging and troubleshooting.
- _Unclear problem tracking_. If the problem solution underperforms, there can be millions of possible culprits to look into, either from the code or from the data, making it hard to ensure solution quality.

In [1] and [2], the authors introduce some best practices and talk about common problems and anti-patterns of learning paradigm development that are worth reading. This essay provides the guiding principles that should be adhered to when adopting learning paradigm in production.

**Data pipeline demonstrates how good the system is**

Data pipeline is one of the very central (if not the most central) components of a learning paradigm system. Because the smartness of the final solution depends on the data used to train it, how such data are stored, labeled and accessed will have direct consequence on the final solution. Also, because most of the ML practitioners' time is munching over the data, how flexible yet principled such data pipeline be will have direct consequence over whether they will quit their job. There are some points to pay attention to when creating a data pipeline:

- There must always be a single source of truth, other immediate data can be derived from it.
- Typically in production, bad data will be cleaned or removed, new data will continuously be added, so it is always important to version and revert the data, both the single source of truth or the derivative data, otherwise you will never be able to reliably compare different solutions.
- Data should be treated by default as dirty, so prepare the sanity check system to flag suspicious data instances.
- Technical solution inform how to label data. Be open-minded when labeling data to anticipate possible technical approaches in the future.

**Isolated reproducible ML components**

Business requirement changes, technology advances, software stacks shift, people come and go. It is important to be able to guard the core technology against such volatilities. An ML solution deployed in production should contains all necessary code and information to be able to replicate solution, even though it comes at the cost of a larger code base. Moreover, because better software stack is released every day, and different versions of software depend on each other in a convoluted manner, it is very easy to have breaking environment dependency somewhere along the line. At the same time, as the field is rapidly evolving, an ML system should not force the ML practitioners into using a fixed set of tools, risking being outdated comparing to competitors. The obvious balance between maintainable system and flexible environment is to make the ML component self-contained and isolated. Current container techniques provide great solution for this, and most of them are free.

**Issues tracking**

Issues tracking is as much about human organization as technical organization. At the heart of an organization, whether ML is used or not used is still for the sole purpose of solving problems. As ML is more complicated, there can be more problems arise during the course of solving the target problem. As a result, it is necessary to have a central place to track all issues, from which the team can be guided with priority and focus.

**Continuous testing and monitoring system**

A lot of state of the art ML solutions are unreliable and brittle. They usually make unexpected incorrect predictions that are hard to explain. Incorrect predictions can be due to bugs, low model capacity, data distribution shift, or data biases. It is important to continuously tests ML solutions as much as possible, especially when new data arrive so that to uncover unseen weaknesses. What to test and monitor for:

- ML models' performance across different sub-set of the data.
- If the ML solution is composed of many smaller ML models, test and benchmark the end-to-end solution.
- Time performance.


**_Conclusion_**: Creating ML production system is hard to get right from the start. There are many components intertwine with each other in complicated ways. The target problems and the envisioned solutions are usually not even clear. It is OK to deal quick-and-dirty with the problem, and think of a suitable ML production system along the way. It is important to have a place where accumulated improvements can be stored, where the inherent uncertainty and messiness of data-dependent solution can be controlled. The final result would be a much better working environment that justifies the cost.
