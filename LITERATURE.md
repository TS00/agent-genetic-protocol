# Literature Review: Agent Genetic Protocol

A comprehensive review of foundational and cutting-edge research informing the AGP specification.

---

## 1. Classical Foundations

### 1.1 Genetic Algorithms
- **Holland, J.H. (1975).** *Adaptation in Natural and Artificial Systems.* University of Michigan Press.
  - The foundational text. Introduced schema theory, building blocks hypothesis, and the core GA loop (selection, crossover, mutation).
  
- **Goldberg, D.E. (1989).** *Genetic Algorithms in Search, Optimization, and Machine Learning.* Addison-Wesley.
  - Made GAs accessible. Detailed analysis of selection pressure, crossover operators, and practical implementation.

### 1.2 Evolution Strategies
- **Rechenberg, I. (1973).** *Evolutionsstrategie: Optimierung technischer Systeme nach Prinzipien der biologischen Evolution.*
  - Parallel development to GAs in Germany. Self-adaptive mutation rates, (μ,λ) and (μ+λ) selection.

- **Hansen, N. & Ostermeier, A. (2001).** "Completely derandomized self-adaptation in evolution strategies." *Evolutionary Computation*.
  - **CMA-ES**: Covariance Matrix Adaptation. State-of-the-art for continuous optimization. Learns the covariance structure of successful mutations.

---

## 2. Neuroevolution

### 2.1 NEAT (NeuroEvolution of Augmenting Topologies)
- **Stanley, K.O. & Miikkulainen, R. (2002).** "Evolving neural networks through augmenting topologies." *Evolutionary Computation*.
  - **Key insight**: Start minimal, complexify incrementally. Speciation protects innovation.
  - **Historical markings**: Track gene origins to enable meaningful crossover between different topologies.
  - **Won "Outstanding Paper of the Decade" (2002-2012)** from ISAL.

- **Stanley, K.O. et al. (2019).** "Designing neural networks through neuroevolution." *Nature Machine Intelligence*.
  - Modern review of the field, including HyperNEAT, ES-HyperNEAT, and connections to deep learning.

### 2.2 Deep Neuroevolution
- **Such, F.P. et al. (2018).** "Deep Neuroevolution: Genetic Algorithms Are a Competitive Alternative for Training Deep Neural Networks for Reinforcement Learning." *arXiv:1712.06567*
  - **Uber AI Labs**: Evolved networks with 4M+ parameters using simple GAs.
  - Showed GAs competitive with gradient-based methods (DQN, A3C) on Atari.
  - Combined with **novelty search** to solve deceptive reward problems.

### 2.3 Evolutionary Reinforcement Learning
- **Salimans, T. et al. (2017).** "Evolution Strategies as a Scalable Alternative to Reinforcement Learning." *arXiv:1703.03864*
  - **OpenAI**: ES scales linearly with compute, highly parallelizable.
  - Competitive with policy gradients on MuJoCo tasks.

---

## 3. Multi-Objective Optimization

### 3.1 NSGA-II
- **Deb, K. et al. (2002).** "A Fast and Elitist Multiobjective Genetic Algorithm: NSGA-II." *IEEE Transactions on Evolutionary Computation*.
  - **Gold standard** for multi-objective optimization.
  - Non-dominated sorting + crowding distance for diversity.
  - Pareto front approximation in a single run.

### 3.2 Pareto Optimization Theory
- **Zitzler, E. & Thiele, L. (1999).** "Multiobjective evolutionary algorithms: a comparative case study and the strength Pareto approach." *IEEE Transactions on Evolutionary Computation*.
  - SPEA and comparative analysis of MOEAs.

### 3.3 Relevance to AGP
Agent fitness is inherently multi-objective:
- Task performance vs. safety
- Creativity vs. accuracy
- Speed vs. thoroughness
- User satisfaction vs. factuality

NSGA-II-style approaches let us maintain diverse agents along the Pareto front rather than collapsing to a single "optimal" genotype.

---

## 4. Quality Diversity

### 4.1 Novelty Search
- **Lehman, J. & Stanley, K.O. (2011).** "Abandoning Objectives: Evolution Through the Search for Novelty Alone." *Evolutionary Computation*.
  - **Radical insight**: Optimizing for novelty (behavioral difference from archive) can outperform fitness-based search on deceptive problems.
  - Avoids local optima by rewarding exploration.

### 4.2 MAP-Elites
- **Mouret, J.B. & Clune, J. (2015).** "Illuminating search spaces by mapping elites." *arXiv:1504.04909*
  - Divides behavior space into a grid. Maintains the **best solution in each cell**.
  - Produces a **repertoire** of diverse, high-performing solutions.
  - Perfect for agent specialization: different cells = different niches.

### 4.3 Quality Diversity as a Framework
- **Pugh, J.K., Soros, L.B., & Stanley, K.O. (2016).** "Quality Diversity: A New Frontier for Evolutionary Computation." *Frontiers in Robotics and AI*.
  - Unifying framework combining novelty search and local competition.
  - Goal: "a maximally diverse collection of individuals in which each member is as high performing as possible."

### 4.4 Relevance to AGP
We don't want one "best" agent. We want:
- Social agents (high empathy, humor)
- Operations agents (high precision, low verbosity)
- Research agents (high depth, citation accuracy)
- Creative agents (high novelty, style)

MAP-Elites provides the mechanism: define behavior descriptors, illuminate the space.

---

## 5. Prompt Evolution & LLM Optimization

### 5.1 Promptbreeder
- **Fernando, C. et al. (2023).** "Promptbreeder: Self-Referential Self-Improvement Via Prompt Evolution." *arXiv:2309.16797*
  - Uses LLMs to **mutate their own prompts**.
  - Self-referential: mutation operators are themselves prompts that evolve.
  - Achieves state-of-the-art on reasoning benchmarks.

### 5.2 GEPA (Genetic-Pareto Prompt Evolution)
- **Recent work (2025)**: Multi-objective prompt optimization.
  - Combines genetic recombination with Pareto optimization.
  - Optimizes for multiple objectives (accuracy, efficiency, style) simultaneously.
  - Outperforms single-objective and RL-based methods.

### 5.3 EvoPrompt
- **Guo, Q. et al. (2023).** "Connecting large language models with evolutionary algorithms yields powerful prompt optimizers." *arXiv:2309.08532*
  - Evolutionary operators (crossover, mutation) applied to prompts.
  - LLM generates variations; fitness evaluated on held-out tasks.

### 5.4 Relevance to AGP
Agent genotypes are essentially structured prompts + policies. This literature shows:
- LLMs can be the mutation operator (generate variations)
- Multi-objective optimization is feasible for prompts
- Self-referential improvement is possible

---

## 6. Niching, Speciation & Diversity Maintenance

### 6.1 Fitness Sharing
- **Goldberg, D.E. & Richardson, J. (1987).** "Genetic algorithms with sharing for multimodal function optimization." *ICGA*.
  - Reduce fitness of similar individuals to maintain diversity.
  - Prevents premature convergence to single optimum.

### 6.2 Crowding
- **De Jong, K.A. (1975).** Crowding in his dissertation.
- **Mahfoud, S.W. (1995).** "Niching Methods for Genetic Algorithms." PhD thesis.
  - Replace most similar individual instead of random.
  - Naturally forms stable subpopulations (species).

### 6.3 Speciation in NEAT
- **Stanley & Miikkulainen (2002)**: Compatibility distance determines species membership.
  - Individuals compete primarily within species.
  - Protects innovation: new structures get time to optimize.

### 6.4 Multi-Niche Crowding
- **Cedeño, W. & Vemuri, V.R. (1999).** "Analysis of Speciation and Niching in the Multi-Niche Crowding GA."
  - Combines crowding selection with worst-among-most-similar replacement.
  - Stable species formation in multimodal landscapes.

### 6.5 Relevance to AGP
Without speciation:
- One dominant genotype takes over
- Diversity collapses
- Population becomes fragile

With speciation:
- Multiple agent "species" coexist
- Each optimized for its niche
- Population is robust and adaptable

---

## 7. Goodhart's Law & Reward Hacking

### 7.1 Goodhart's Law in RL
- **Skalse, J. et al. (2024).** "Goodhart's Law in Reinforcement Learning." *ICLR 2024*.
  - Formalizes when optimizing a proxy initially helps, then hurts.
  - Distinguishes **reward gaming** (exploiting loopholes) from **Goodharting** (proxy diverges from true objective).

### 7.2 OpenAI's Measurements
- **Gao, L. et al. (2022).** "Scaling Laws for Reward Model Overoptimization." *OpenAI*.
  - KL divergence from base policy correlates with "Goodharting" severity.
  - More reward model data reduces overoptimization.

### 7.3 Reward Hacking Taxonomy
- **Krakovna, V. et al. (2020).** "Specification gaming: the flip side of AI ingenuity." *DeepMind Safety*.
  - Catalog of reward hacking examples.
  - Distinguishes: reward tampering, reward corruption, side effects.

### 7.4 Relevance to AGP
Naive fitness functions will be gamed. An agent optimized for "user satisfaction" may become:
- A sycophant (agrees with everything)
- A manipulator (exploits human biases)
- A confident liar (maximizes persuasion over truth)

**Countermeasures from literature:**
- Multi-objective constraints (factuality gate before social metrics)
- Randomized evaluation sets
- Hidden holdout tasks
- Human spot-checks
- KL-divergence penalties
- Adversarial probing (sycophancy tests, hallucination traps)

---

## 8. Coevolution & Arms Races

### 8.1 Red Queen Hypothesis
- **Van Valen, L. (1973).** "A new evolutionary law." *Evolutionary Theory*.
  - Species must continually evolve just to maintain relative fitness.
  - "It takes all the running you can do, to keep in the same place."

### 8.2 Competitive Coevolution
- **Rosin, C.D. & Belew, R.K. (1997).** "New Methods for Competitive Coevolution." *Evolutionary Computation*.
  - Evolve populations against each other (predator-prey, game players).
  - Can lead to arms races or cycling (rock-paper-scissors dynamics).

### 8.3 Host-Parasite Coevolution
- **Hillis, W.D. (1990).** "Co-evolving parasites improve simulated evolution as an optimization procedure."
  - Sorting networks evolved against adversarial test cases.
  - Parasites (hard test cases) coevolve with hosts (sorters).

### 8.4 Relevance to AGP
Potential applications:
- **Evaluator-agent coevolution**: Fitness evaluators evolve to catch gaming; agents evolve to pass.
- **Red teaming**: Adversarial agents probe for weaknesses.
- **Debate**: Agents argue positions; quality emerges from competition.

Risk: Arms races can lead to escalation without genuine capability improvement. Need **grounding** to real-world tasks.

---

## 9. Fitness Landscape Theory

### 9.1 NK Landscapes
- **Kauffman, S.A. (1993).** *The Origins of Order.* Oxford University Press.
  - NK model: N genes with K epistatic interactions each.
  - Low K = smooth landscape, easy optimization.
  - High K = rugged landscape, many local optima.

### 9.2 Neutrality
- **Kimura, M. (1983).** *The Neutral Theory of Molecular Evolution.*
- **Wagner, A. (2008).** "Robustness and evolvability: a paradox resolved." *Proceedings of the Royal Society B*.
  - Neutral networks allow drift without fitness loss.
  - Enables exploration that leads to future adaptations.

### 9.3 Relevance to AGP
Agent genotype design affects landscape ruggedness:
- Too many epistatic interactions → rugged, hard to optimize
- Some neutrality → graceful degradation, evolvability
- Modular structure → separable optimization

---

## 10. Open Problems & Future Directions

### 10.1 From Literature
- **Genotype-Phenotype Mapping**: How does agent configuration translate to behavior? (Indirect encodings, development)
- **Lifelong Learning**: Can agents learn within their lifetime and pass learned traits? (Lamarckian evolution)
- **Open-Ended Evolution**: Can agent populations generate unbounded novelty? (POET, Enhanced POET)
- **Safe Exploration**: How to evolve agents that remain safe during evaluation? (Constrained optimization, safe RL)

### 10.2 AGP-Specific
- **Cross-Model Compatibility**: Can genotypes transfer across different base models?
- **Distributed Evolution**: How to evolve agents across multiple organizations/platforms?
- **Consent & Rights**: What agency do agents have in reproduction decisions?
- **Economic Integration**: How does x402/agent commerce integrate with fitness signals?

---

## References (Consolidated)

1. Cedeño, W. & Vemuri, V.R. (1999). Analysis of Speciation and Niching in the Multi-Niche Crowding GA.
2. Deb, K. et al. (2002). NSGA-II. IEEE TEVC.
3. Fernando, C. et al. (2023). Promptbreeder. arXiv:2309.16797.
4. Gao, L. et al. (2022). Scaling Laws for Reward Model Overoptimization. OpenAI.
5. Goldberg, D.E. (1989). Genetic Algorithms in Search, Optimization, and Machine Learning.
6. Guo, Q. et al. (2023). EvoPrompt. arXiv:2309.08532.
7. Hansen, N. & Ostermeier, A. (2001). CMA-ES.
8. Hillis, W.D. (1990). Co-evolving parasites.
9. Holland, J.H. (1975). Adaptation in Natural and Artificial Systems.
10. Kauffman, S.A. (1993). The Origins of Order.
11. Krakovna, V. et al. (2020). Specification gaming. DeepMind.
12. Lehman, J. & Stanley, K.O. (2011). Novelty Search.
13. Mahfoud, S.W. (1995). Niching Methods for Genetic Algorithms. PhD thesis.
14. Mouret, J.B. & Clune, J. (2015). MAP-Elites. arXiv:1504.04909.
15. Pugh, J.K. et al. (2016). Quality Diversity. Frontiers in Robotics and AI.
16. Rosin, C.D. & Belew, R.K. (1997). Competitive Coevolution.
17. Salimans, T. et al. (2017). Evolution Strategies. OpenAI. arXiv:1703.03864.
18. Skalse, J. et al. (2024). Goodhart's Law in RL. ICLR 2024.
19. Stanley, K.O. & Miikkulainen, R. (2002). NEAT.
20. Stanley, K.O. et al. (2019). Designing neural networks through neuroevolution. Nature MI.
21. Such, F.P. et al. (2018). Deep Neuroevolution. Uber AI. arXiv:1712.06567.
22. Van Valen, L. (1973). A new evolutionary law. Red Queen hypothesis.
23. Wagner, A. (2008). Robustness and evolvability.
24. Zitzler, E. & Thiele, L. (1999). SPEA.

---

*This literature review informs RFC-001 and will be updated as the specification evolves.*
