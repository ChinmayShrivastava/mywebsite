---
title: Big v/s small models for mechanical simulations
author: Chinmay Shrivastava
pubDatetime: 2025-03-02T23:15:31Z
slug: foundation-models-for-mechanics
featured: true
draft: true
tags:
  - ai
  - physics
  - meche
description: Historically, AI has been useful in optimization of physical products. But does the emergance of foundational models change how deep learning
is applied to mechanics?
---

Why do you need to train a big foundational model?

- To capture more design parameters

Is it important to capture a lot of design parameters? How do you quantify parameters and how many parameters is enough?

- There can be a lot of parameters in a design and simple AI models can

Key Questions to Answer by the end:

1. Do we really need physics based AI models for simulations?
2. What are the best usecases and why?
3. Why would you want to train a large model? Why would it be okay for it to just be a geometric model v/s why it would need to be pretrained also on physics?
4. Would it benefit if it is multimodal in any way?

---

Physics that we know are essentially mathematical approximations of phenomena that we observe; either in our daily lives or during experimentations or theoricital
speculations backed by strong reasoning. While some are ageless, a lot of these approximations are regularly disproven or updated with better approximations based
on new findings. It is practically impossible for these approximations to perfectly predict the real world observations, which are affected by physical
uncertainties, non-linearities, and human error.

But, while imperfect, these approximations allow engineers and researchers to "predict" behaviour of a system before the observation itself. Among other things,
this primarily eliminates expensive failures by favoring theoritical calculations before physical tests. In Mechanical Engineering, this predominantly manifests
itself as numerical simulations. As in the name, numerical simulations are numerical methods to approximate physics that are defined using PDEs.

While 50 years ago, these results were calculated on paper by hand, technological advancements fueled by CPUs lead the domain complexity of these approximations
to increase. This means, that if they were calculate how a beam would bend under force, they could now calculate how a realistic airplane wing (with all its
complex curvatures) would bend under force.

The domain complexity grew further as CPUs got stronger over the last few decades, and the numerical solvers (algorithms for approximations) improved and shaved off
runtime. Recently, some mathematical models can approximate fluid based simulations using GPU parallelization improving the run time by 3-10x. Although, for most of
the applications CPU based implicit simulations, developed and optimized over decades still remain dominant.

And while the run times have generally improved over time, these still are classified as slow and require the engineer to simplify the domain of the problem to balance
out cost and simulation effectiveness. In mechanical engineering, the optimization problem is finding the optimal paraters in a parameterized design domain. A simple
design with 10 parameters, each of which can hold 10 values leads the design space to have 10^10 variations which is a reasonably conservative assumption. In the real
world, the parameters can be as large as 200 (or more) and vary within continuous bounds. Instead of blindly performing random monte-carlo searches to find the most
optimal solution, engineers carefully handpick a few sets of parameters to test (called Design of Experiments or DoE) based on pareto principle that gets them to 80%
of the optimal design.

Further simulations, generally offer diminishing returns making it wasteful. And so, the engineers choose the best design based on the DoE and start making
granular optimizations to it. From here, most simulations are low frequency and are required for validation purposes only. This means, they take longer to run
and require high accuracy.

Although, this process works well, in the same way physics approximations can be revised for better outputs, it can improve further.

### The problem of time and cost

While engineers can effectively reduce the combinatorial design space problem through heuristics and experience, the overall process still remains slow and time
consuming due to the implicit complexity of numerical simulations. A few products (like Ansys Discovery) offer tools for real time approximations enabling engineers
to rapidly test out design changes. However, these approximations suffer from inadequate approximations as they are based on highly reduced physical approximations,
and aren't easily applicable to highly nonlinear problems.

Further, it simplifies designs removing any small geometric features without user control and uses voxel based methods that severely affect the accuracy of the
approximations. Simulating complex physics requiring high-fidelity in the design therefore still is limited by computationally intensive numerical solvers.

https://cfdland.com/ansys-fluent-vs-ansys-discovery/
https://www.reddit.com/r/ANSYS/comments/t7ciha/is_ansys_discovery_good_for_cfd/
https://www.softwareadvice.com/3d-cad/ansys-discovery-profile/reviews/
https://storage.ansys.com/doc_assets/kil_docs/Known_Issues_and_Limitations_192.pdf
https://www.reddit.com/r/fea/comments/drvr59/ansys_discovery_live_vs_other_top_market/
https://www.softwareadvice.com/3d-cad/ansys-discovery-profile/
https://www.ansys.com/content/dam/web/academic/education-resources/resources/intro-meshing-papitmdien24.pdf
https://www.youtube.com/watch?time_continue=26&v=_8JlfuN0WQc&embeds_referring_origin=https://www.perplexity.ai

### The problem with design of experiments

While tools like Ansys Discovery are great for design space exploration (with aforementioned caveats), they don't pertain to parameteric optimization. Once the design
parameters are set through design exploration, through careful design of experiments an engineer accesses parametric sensitivities while ensuring you sample the whole
space for comprehensive coverage.

Automated tools (like Ansys OptiSlang or Simcenter's HEEDS) utilize AI and heuristic based algorithms to perform autonomous design optimization through parametric changes. However, it is not
foolproof. These tools suffer from noisy simulations and require geometry simplifications to avoid mesh failure for successful autonomous optimization. Robustness of the
optimizer becomes computationally intensive if the total number of parameters exceeds ~15. Therefore, it requires sacrificing precision. Further, highly non-linear problems
are difficult for these tools to optimize and require careful sampling strategy. These tools have a tendency of chasing numerical ghosts in the optimization space, e.g.
negative thickness value, if not configured properly. The sensitivity analysis might misidentify important variables optimizing for the wrong set of parameters.
Further robustness to these issues requires higher sampling in noisy regions, performing high fidelity simulations which require more resources and time. So critical
geometries require for other studies to get mesh independence for reliable optimization results.

https://innovationspace.ansys.com/forum/forums/topic/how-to-improve-the-results-of-an-optimization-in-optislang/
https://library.dynardo.de/fileadmin/Material_Dynardo/WOST/Paper/wost6.0/Presentation_Veiz.pdf
https://library.dynardo.de/fileadmin/Material_Dynardo/WOST/Paper/wost12.0/WOST2015_Workshop_RDO.pdf
https://www.leapaust.com.au/blog/cfd/next-generation-robust-design-optimisation-with-ansys-optislang/
https://www.padtinc.com/2020/06/03/an-ansys-optislang-overview-and-optimization-example-with-ansys-icepak/
https://optics.ansys.com/hc/en-us/articles/19415785234195-Automated-Optomechanical-STOP-Analysis
https://www.ansys.com/content/dam/product/platform/optislang/optislang-brochure.pdf
https://www.ansys.com/blog/perform-efficient-robust-design-optimization-speos
https://ieeexplore.ieee.org/abstract/document/10026117
https://www.cadfem.net/fileadmin/user_upload/05-cadfem-informs/resource-library/ANSYS_optiSLang_eng_P_2016_Web.pdf
https://www.ansys.com/blog/optimize-design-simulation-with-ai-ml-metamodeling
https://fastwayengineering.com/ansys-software/optislang-ai/
https://www.ansys.com/blog/how-to-design-better-products
https://simutechgroup.com/introduction-to-optimization-and-robust-design-using-ansys-optislang/
https://edrmedeso.com/article/ansys-optislang-guide/

### The problem with simplification

Due to the computational intensive solvers, simplification of the design favours optimization. Engineers simplify geometries through removing fine details, removing
non-critical components and side-lining non-sensitive parameters. By simplifying the topology, and reducing the parametric space, performing a pareto front parametric
optimization becomes feasible. However, simplification leads to suboptimal results.

The three problems, time and cost, DoE, and simplification all make it difficult for a mechanical optimization engineer to reach the optimal design. While AI proposes
to alleviate a lot of these problems, it is also important to understand how the other end of the spectrum look like.

### The problem with Generative Designs and Algorithmic Topology Optimization

########

We understand that performing design exploration and optimization manually leads to suboptimal results due to resource constraints and heuristic search through the
combinatorial space. On the other hand, algorithmic generative designs and topology optimization techniques while produce effective results, they too suffer from
high compute requirements and are unable to generate easily manufacturable outputs.

Deep Learning models offer a possibility to do both at the same time.

## The third way out

########

There are reasons to believe that deep learning

--- Neo Founder's profile
During undergrad at IIT Roorkee, I pursued Mechanical Engineering. With my focus on computational mechanics, I worked mostly on simulating elastic actuators with AI, and wave propagation through metals among other things.

Later at Brown, I got a part-patent ownership on a mechanical device. Additionally, I started building AI products. Over the last few years, I have built 10s of AI products. The most noteworthy of them would be the training of a knowledge graph over the internet that was used by 1200 people to generate personalized learning roadmaps. This was 6 months before ChatGPT was publicly announced.
