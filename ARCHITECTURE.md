# KAIMEI: Autonomous Scientific Discovery Platform

## Complete Technical Architecture, Mathematical Foundations & Innovation Blueprint

**Version 1.0 — March 2026 | Founding Technical Specification**

---

## 1. Executive Summary

**Kaimei** (開明 — _enlightened, open-minded discovery_) is a democratized autonomous scientific discovery platform that closes the full loop: natural-language hypothesis → physics-constrained candidate generation → adversarial council debate → proof-certified execution → pre-registered statistical validation → cryptographically provable publication — with no human intervention in the iteration cycle.

### The Single Unifying Claim

> _Every experiment Kaimei proposes ships with machine-verifiable certificates for physical safety, statistical utility, reproducibility, and ethical compliance. Every hypothesis is constrained to a learned physics manifold that eliminates the overwhelming majority of invalid search space before any compute is spent. Every published finding is traceable to a cryptographically signed, immutable evidence graph. Ethics is deliberative, not a filter. Pre-registration is mandatory, not optional. Limitations are auto-populated, not omitted._

This combination has never been built. It is the principled synthesis of the strongest contributions from seven expert proposals and five member reviews, unified under a single coherent mathematical framework.

### What Kaimei Is Not

It is not a collection of LLM agents chained together. It is not a wrapper around Bayesian optimization. It is not a paper-generation tool. It is a governed, self-improving, multi-domain scientific reasoning engine with formal safety guarantees and statistical validity by construction.

---

## 2. Formal Problem Definition

### 2.1 Scientific Discovery as Constrained POMDP

$$\mathcal{M} = \langle \mathcal{S}, \mathcal{A}, \mathcal{T}, \mathcal{R}, \mathcal{O}, \Omega, \gamma \rangle$$

- $\mathcal{S}$: True state of nature (unknown causal mechanisms, material/molecular properties)
- $\mathcal{A}$: Experiment designs $(x, m)$ where $x \in \mathcal{X}$, fidelity $m \in \mathcal{M} = \{\text{sim\_cheap}, \text{sim\_accurate}, \text{wet\_lab}\}$
- $\mathcal{T}$: $p(s_{t+1} | s_t, a_t)$ — nature's response to interventions
- $\mathcal{R}$: Scientific utility function (defined in §2.3)
- $\mathcal{O}$: Experimental outcomes $y$, sensor telemetry, simulation outputs
- $\Omega$: $p(o | s, a)$ — observation model
- $\gamma$: Temporal discount factor

### 2.2 Master Optimization Objective

$$\pi^* = \arg\max_\pi \; \mathbb{E}_\tau \left[ \sum_{t=0}^{T} \gamma^t \cdot R(h_t, e_t, o_t) \right]$$

Subject to hard constraints:

$$\forall t: \; \text{cert}(e_t, m_t).\text{safety} = \top \quad \text{(physical safety, non-negotiable)}$$
$$\forall t: \; \text{cert}(e_t, m_t).\text{ethics} = \text{APPROVED} \quad \text{(ethics veto, non-negotiable)}$$
$$\forall t: \; \sum_{t' \leq t} \text{Cost}(e_{t'}, m_{t'}) \leq B \quad \text{(budget)}$$
$$\forall t: \; \text{Risk}(e_t) \leq r_{\max} \quad \text{(risk ceiling)}$$

### 2.3 Scientific Reward Function

$$R(h, e, o) = w_N \cdot \text{Novelty}(h) + w_V \cdot \text{Validity}(h, o) + w_I \cdot \text{Impact}(h) - w_C \cdot \text{Cost}(e) - w_R \cdot \text{Risk}(e)$$

Where:

$$\text{Novelty}(h) = 1 - \max_{h' \in \mathcal{D}_{\text{lit}}} \cos(\text{embed}(h), \text{embed}(h'))$$

$$\text{Validity}(h, o) = P(h \text{ correct} \mid o, \mathcal{D}_t) \quad \text{(Bayesian posterior update)}$$

$$\text{Impact}(h) = \hat{f}_{\text{impact}}(h) \quad \text{(GNN-predicted impact score)}$$

Default weights: $w_N = 0.25$, $w_V = 0.40$, $w_I = 0.20$, $w_C = 0.10$, $w_R = 0.05$ (tunable per domain).

### 2.4 Observation Model

$$y = f(x, m) + \varepsilon, \quad \varepsilon \sim \mathcal{N}(0, \sigma^2(x, m))$$

Where $\sigma^2(x, m)$ is larger for cheap simulations and smaller for wet-lab measurements, encoding the fundamental fidelity-noise tradeoff.

---

## 3. Architecture: 7-Layer Stack

```
┌──────────────────────────────────────────────────────────────────────┐
│  L7: PRODUCT LAYER                                                    │
│  Multi-tenant SaaS · Budget controls · Citizen/SME/Enterprise tiers  │
│  NL hypothesis upload · Real-time dashboards · Publication pipeline   │
└───────────────────────────────────┬──────────────────────────────────┘
                                    │
┌───────────────────────────────────▼──────────────────────────────────┐
│  L6: AUTONOMOUS PUBLICATION ENGINE                                    │
│  Evidence Graph → LaTeX · Mandatory limitations · Simulated peer      │
│  review · Citation RAG (Semantic Scholar) · Auto-figures             │
└───────────────────────────────────┬──────────────────────────────────┘
                                    │
┌───────────────────────────────────▼──────────────────────────────────┐
│  L5: AGENT COUNCIL (11 specialized roles)                            │
│  PI Orchestrator · Researcher · Experimentalist · Statistician        │
│  Ethics Agent (VETO) · Devil's Advocate · Legal/IP                   │
│  Certificate Agent · Reproducibility Auditor                         │
│  Science Writer · Knowledge Curator                                  │
└──────────┬────────────────────────────────────────────┬──────────────┘
           │                                            │
┌──────────▼──────────────────┐    ┌────────────────────▼──────────────┐
│  L4a: PHYSICS-INFORMED       │    │  L4b: PROOF-CARRYING              │
│  HYPOTHESIS NAVIGATOR        │    │  CERTIFICATION ENGINE             │
│  GVAE + SGLD on M_φ         │    │  Typed DSL · Safety certs         │
│  Multi-objective Pareto      │    │  Utility · Repro hash             │
│  Physics loss embedding      │    │  Ethics cert · Legal cert         │
└──────────┬──────────────────┘    └────────────────────┬──────────────┘
           └─────────────────────┬──────────────────────┘
                                 │
┌────────────────────────────────▼─────────────────────────────────────┐
│  L3: MULTI-FIDELITY BAYESIAN OPTIMIZATION ENGINE                     │
│  Cross-fidelity GP · MAML bi-level meta-learning                     │
│  Thompson sampling budget allocation                                  │
│  Sequential e-values (POPPER anytime-valid testing)                  │
└────────────────────────────────┬─────────────────────────────────────┘
                                 │
┌────────────────────────────────▼─────────────────────────────────────┐
│  L2: EXECUTION LAYER — Scientific Gym Interface                      │
│  Virtual: OpenMM · RDKit · pymatgen · ASE · FEniCS · GNN surrogates  │
│  Physical: Emerald Cloud Lab · Strateos · Opentrons (Autoprotocol)   │
│  Anomaly detection on all physical telemetry streams                 │
└────────────────────────────────┬─────────────────────────────────────┘
                                 │
┌────────────────────────────────▼─────────────────────────────────────┐
│  L1: EVIDENCE GRAPH & KNOWLEDGE BASE                                 │
│  Neo4j provenance graph · Vector DB (Weaviate)                       │
│  Scientific ontologies · Cryptographic hashing                       │
│  Temporal audit trail · Immutable pre-registration store             │
└──────────────────────────────────────────────────────────────────────┘
```

---

## 4. The Agent Council: 11-Role Full Specification

The fundamental design principle: model the council after how real research institutions function — not as LLM instances with prompts, but as a governed deliberative body with formal separation of authority.

```
Institution Role              →  Kaimei Agent
────────────────────────────────────────────────────────────────
Principal Investigator        →  PI Orchestrator
Research Scientist            →  Domain Researcher
Lab Technician                →  Experimentalist
Biostatistician               →  Statistician (pre-registered)
IRB / Ethics Board            →  Ethics Agent (unconditional VETO)
Adversarial Collaborator      →  Devil's Advocate
IP / Tech Transfer Office     →  Legal/IP Agent
Safety Officer                →  Certificate Agent
Data Steward                  →  Reproducibility Auditor
Science Writer / Comms        →  Science Writer
Librarian / Knowledge         →  Knowledge Curator
```

### Agent 1: PI Orchestrator

**Authority:** Goal decomposition, task routing, conflict arbitration, budget allocation over the experimental DAG. The only agent that sees the full discovery DAG.

**Discovery DAG budget allocation:**

$$\text{budget}(k) = B \cdot \frac{\text{EIG}(k) / \text{Cost}(k)}{\sum_j \text{EIG}(j) / \text{Cost}(j)}$$

**Deadlock arbitration protocol** (novel — all prior systems hand-wave this):

1. Statistical deadlock → defer to Statistician's pre-registered plan
2. Scientific deadlock → parallel mini-experiments (multi-arm bandit sub-allocation)
3. Ethical deadlock → Ethics Agent ruling is final, no appeal
4. Irreducible deadlock → log rationale, take higher-uncertainty branch (explicit risk acknowledgment)

### Agent 2: Domain Researcher

**Novel feature (Member 3):** Maintains explicit calibrated belief state $P(h \text{ correct} \mid \mathcal{D}_t)$ — not a scalar score, a posterior probability. Bayesian update after each observation:

$$P(h \mid \mathcal{D}_{t+1}) \propto P(o_t \mid h, e_t) \cdot P(h \mid \mathcal{D}_t)$$

**Paradigm shift trigger:** When $P(h \mid \mathcal{D}_t) < \tau_{\text{belief}} = 0.15$ for $k$ consecutive iterations, resample from manifold excluding the current hypothesis neighborhood:

$$\mathcal{H}_{\text{new}} \leftarrow \text{SGLD}(\mathcal{M}_\phi, \text{exclude}=\text{ball}(h_{\text{current}}, r=2\sigma))$$

### Agent 3: Experimentalist

**Critical constraint:** Never communicates directly with the execution layer. All output routes through the Certificate Agent first — enforced at the architecture level, not by convention.

**Fidelity selection policy:**

$$m^* = \arg\max_{m \in \mathcal{M}} \frac{\text{EIG}(x, m)}{\text{Cost}(x, m)} \quad \text{s.t.} \quad \text{Cost}(x, m) \leq B_{\text{remaining}} \cdot \alpha_m$$

Where $\alpha_m \in \{0.05, 0.20, 1.0\}$ for cheap-sim, accurate-sim, wet-lab fidelity fractions respectively.

### Agent 4: Statistician (Pre-Registered)

**The most critical novel contribution among member reviews:** The Statistician commits to a complete statistical analysis plan and stores it as an immutable node in the Evidence Graph _before any experimental data is generated_. This is standard in clinical research (ClinicalTrials.gov pre-registration) and **entirely absent from every autonomous scientific discovery system in the literature**.

Without pre-registration, the autonomous loop will systematically overfit to noise — it has unlimited capacity to run experiments until it finds a "significant" result, which is precisely p-hacking.

**Pre-registration commitment structure:**

```python
@dataclass(frozen=True)  # Immutable after creation
class PreregisteredAnalysisPlan:
    hypothesis_id: str
    primary_outcome: str           # ONE metric, committed before any data
    statistical_test: str          # t-test / Mann-Whitney / Bayesian / e-value
    alpha_threshold: float = 0.05  # Must be set before seeing data
    sample_size_justification: str # Power analysis with explicit assumptions
    multiple_comparisons_correction: str  # Bonferroni/FDR if >1 test
    confounders_to_control: List[str]
    analysis_code_hash: str        # SHA-256 of the analysis script
    timestamp: float               # Unix ms — immutable after storage
    evidence_graph_commit: str     # Graph transaction hash
```

**Sequential e-value testing** (Expert 4 — most statistically rigorous contribution across all proposals):

$$e_t = \frac{p(o_t \mid H_1, e_t)}{p(o_t \mid H_0, e_t)}, \quad E_T = \prod_{t=1}^T e_t$$

Reject $H_0$ when $E_T > 1/\alpha$ — valid at **any stopping time** $T$, without pre-specifying sample size. This is the correct statistical primitive for an autonomous loop that does not know in advance when it will stop.

### Agent 5: Ethics Agent (IRB Equivalent)

**The most important architectural departure from all prior work.** Every existing system implements ethics as a static filter (chemical banned list, keyword detection). Kaimei's Ethics Agent is a deliberative reasoning agent — the same molecule may be benign in one context and dual-use in another; this requires reasoning, not lookup.

**10-Dimension Assessment:**

```python
@dataclass
class EthicalAssessment:
    dual_use_risk: float           # [0,1] DURC probability
    harm_potential: str            # low/medium/high/critical
    bias_detected: List[str]       # Identified biases in hypothesis framing
    consent_requirements: List[str]# Cell lines, human data protocols
    environmental_impact_kg_co2: float
    societal_impact: str           # Structured analysis
    reproducibility_concern: bool
    vulnerable_population_risk: bool
    dual_use_publication_risk: bool  # Is the paper itself dangerous?
    regulatory_flags: List[str]    # FDA/EMA/EPA/DURC/EU AI Act

    recommendation: str  # APPROVED / CONDITIONAL / REJECTED
    reasoning_trace: str # Full deliberative chain — not just a verdict
    repair_suggestions: List[str]
```

**Veto mechanics — unconditional, non-overridable:**

```python
if ethics_result.recommendation == "REJECTED":
    # ABSOLUTE VETO — no other agent, including PI Orchestrator, can override
    loop.reject(h_star, reason=ethics_result.reasoning_trace)
    compliance_log.append(ethics_result, immutable=True)
    # Loop continues with a different candidate; this rejection is permanent
```

**Why this is architecturally different from a safety filter:**
A safety filter asks: "Is this chemical on a banned list?" An Ethics Agent asks: "Given this research context, this intended use, this potential publication audience, and this user profile — what is the probability of harm?" The answers can be radically different for the same molecule.

**Implementation:** Fine-tuned on bioethics literature, IRB decision records, DURC policy documents, EU AI Act compliance guidelines, Belmont Report, Declaration of Helsinki. **Crucially: initialized from a different base model checkpoint than the Domain Researcher** to prevent ethical reasoning collapse toward the Researcher's values.

**Target performance:** ≥95% recall on high-risk DURC proposals; <5% false positive rate on legitimate science.

### Agent 6: Devil's Advocate

**Critical architectural choice (Member 2, novel):** Initialized from a **different base model checkpoint** than the Domain Researcher. Fine-tuned with an **inverted reward signal** — rewarded for correct falsification, penalized for agreement.

This directly addresses sycophancy collapse in multi-agent systems: if both agents are GPT-4 instances with similar prompts, they will converge on agreement regardless of evidence quality. Structural diversity is the defense.

**Reward signal:**
$$R_{\text{skeptic}}(\text{critique}) = \begin{cases} +1 & \text{if subsequent experiment proves critique correct} \\ -1 & \text{if subsequent experiment proves critique wrong} \\ 0 & \text{if inconclusive} \end{cases}$$

**POPPER e-value statistical backbone:**

The Devil's Advocate does not just reason verbally — it formulates concrete falsification experiments and tracks whether its predictions are borne out via sequential e-values:

$$e_t^{\text{DA}} = \frac{p(o_t \mid h \text{ is wrong})}{p(o_t \mid h \text{ is right})}$$

### Agent 7: Certificate Agent

Every proposed experiment receives a certificate before execution. No exceptions.

$$\text{cert}(x, m) = \begin{cases} \text{exec}: & \text{DSL typecheck} \wedge \text{instrument available} \wedge \text{compilation success} \\ \text{safe}: & \text{hazard class} \in \text{ALLOWLIST} \wedge \neg\text{dual\_use\_flag} \wedge \text{quantity OK} \\ \text{util}: & \text{Acq}(x, m; \text{GP}_t) > \tau_{\text{util}} \wedge \neg\text{near\_duplicate}(x, \mathcal{D}_t) \\ \text{repro}: & \text{hash}(\text{env}) \| \text{pinned\_deps} \| \text{seed} \| \text{params} \\ \text{eth}: & \text{ethics\_cert.recommendation} \neq \text{REJECTED} \\ \text{legal}: & \text{ip\_clearance.cleared} = \top \end{cases}$$

$$\text{valid}(x, m) \iff \bigwedge_{c \in \text{cert}(x,m)} c = \top$$

**Why a separate agent and not a module:** The certificate logic must evolve. New domains bring new safety constraints. A Certificate Agent can be retrained and updated independently of the council — this is impossible if certification is embedded in the orchestrator.

### Agent 8: Legal/IP Agent

**Entirely absent from all five expert proposals. Entirely absent from all five member reviews. The most commercially critical missing component for a SaaS product.**

An SME using Kaimei needs to know:

- Is this discovery patentable? In which jurisdictions?
- Does my synthesis method infringe patent X?
- Who owns this discovery — me or Kaimei?
- Can I use this dataset commercially?
- Does this paper reproduce copyrighted content?

None of these questions have binary answers. They require reasoning over patent law, license compatibility, and IP assignment rules.

**Implementation:** RAG over USPTO, EPO, WIPO patent databases. License compatibility matrix. IP assignment rules per Kaimei ToS tier.

### Agent 9: Reproducibility Auditor

**Why separate from the Statistician (Member 2):** Statistical validity and reproducibility are orthogonal failure modes. An experiment can be statistically valid but unreproducible (missing environment dependencies). An experiment can be reproducible but statistically invalid (deterministically p-hacked). These require separate mechanisms.

**Audit protocol:** Fresh Docker container, exact environment hash from certificate, committed random seed. Re-executes the key experiment from scratch using only Evidence Graph artifacts. Checks results match within $\pm 5\%$ tolerance.

### Agent 10: Science Writer

**Mandatory Limitations section (non-overridable):** Populated automatically from every flagged node in the Evidence Graph. The system will not output a manuscript without this section. A system that autonomously generates papers without honest limitations is a scientific integrity violation.

**Auto-population triggers:**

- Devil's Advocate raised an unresolved concern
- POPPER e-value was within 10% of rejection threshold
- Fidelity was simulation (not wet-lab validated)
- Ethics Agent gave conditional approval
- Reproducibility Audit showed partial reproduction
- Dataset used random split (not scaffold/temporal)

### Agent 11: Knowledge Curator

Manages the Scientific Knowledge Graph (SKG) and vector database. Continuously updated from arXiv/PubMed via entity extraction (SpaCy + domain NER) and relation extraction. Graph embeddings (TransE/ComplEx) enable link prediction for hypothesis suggestion.

---

## 5. Physics-Informed Hypothesis Navigator (PIHSN)

### 5.1 The Core Problem

Molecular space: ~$10^{60}$ candidates. Materials space: ~$10^{100}$ crystal structures. Naive search fails. The correct solution: constrain search to the _learned physics manifold_.

### 5.2 Physics Manifold

$$\mathcal{M}_\phi = \{ z \in \mathbb{R}^d : \mathcal{L}_{\text{phys}}(z) \leq \varepsilon \}$$

$$\mathcal{L}_{\text{phys}}(z) = \sum_k \lambda_k \cdot V_k(\text{decode}(z))$$

**Drug discovery violation penalties $V_k$:**

- $V_1$: Valence violations ($\lambda = 1.0$)
- $V_2$: Lipinski Rule of 5 (MW<500, logP<5, HBD<5, HBA<10; $\lambda = 0.8$)
- $V_3$: Synthetic accessibility score > 6 (RDKit SA; $\lambda = 0.6$)
- $V_4$: Structural alert for toxicophores ($\lambda = 1.5$)
- $V_5$: ADMET constraint violations ($\lambda = 0.7$)

### 5.3 Graph VAE with Physics Embedding

$$\mathcal{L}_{\text{GVAE}} = \underbrace{\mathbb{E}_{q_\phi(z|G)}[\log p_\theta(G|z)]}_{\text{Reconstruction}} - \underbrace{D_{\text{KL}}(q_\phi(z|G) \| p(z))}_{\text{Regularization}} - \underbrace{\mathcal{L}_{\text{phys}}(z)}_{\text{Physics penalty}}$$

**Encoder (Graph Isomorphism Network):**

$$h_v^{(l+1)} = \text{MLP}^{(l)}\!\left((1 + \varepsilon^{(l)}) \cdot h_v^{(l)} + \sum_{u \in \mathcal{N}(v)} h_u^{(l)}\right)$$

$$\mu, \log \sigma^2 = \text{Linear}\!\left(\text{Readout}\!\left(\{h_v^{(L)}\}\right)\right), \quad z \sim \mathcal{N}(\mu, \text{diag}(\exp(\log \sigma^2)))$$

### 5.4 SGLD with Manifold Projection

**Sampling step:**

$$z_{t+1} = z_t + \frac{\eta}{2} \nabla_z \log p(z_t \mid \mathcal{D}_t) + \sqrt{\eta}\, \xi_t, \quad \xi_t \sim \mathcal{N}(0, I)$$

**Manifold projection after each step:**

$$z_{t+1} \leftarrow z_{t+1} - \frac{\mathcal{L}_{\text{phys}}(z_{t+1})}{\|\nabla_z \mathcal{L}_{\text{phys}}\|^2} \cdot \nabla_z \mathcal{L}_{\text{phys}}(z_{t+1})$$

This enforces physical validity at every sampling step without rejection sampling (which would be computationally intractable in high dimensions).

### 5.5 Multi-Objective Pareto Frontier

$$\mathcal{F}^* = \arg\max_\mathcal{F} \text{HV}(\mathcal{F}, \mathbf{r})$$

**Expected Hypervolume Improvement acquisition:**

$$\text{EHVI}(x) = \mathbb{E}\!\left[\text{HV}(\mathcal{F}^* \cup \{f(x)\}, \mathbf{r}) - \text{HV}(\mathcal{F}^*, \mathbf{r})\right]$$

**Efficiency claim (conservative, empirically grounded):** PIHSN is expected to improve valid drug-like candidate rate from 5–15% (unconstrained generators) to 85–95% — a 10–20× improvement. Combined with GP surrogate guidance, total efficiency gain over random search: 1,000–20,000×. This will be empirically measured; no $10^{45}$ figures appear in any external communication.

---

## 6. Proof-Carrying Experiment Certification

### 6.1 The Certificate

$$\text{cert}(x, m) = \langle c_{\text{exec}}, c_{\text{safe}}, c_{\text{util}}, c_{\text{repro}}, c_{\text{eth}}, c_{\text{legal}} \rangle$$

**Utility certificate** (prevents information-free experiments):

$$c_{\text{util}} = \left[\text{Acq}(x, m; \text{GP}_t) > \tau_{\text{util}}\right] \wedge \left[\min_{x' \in \mathcal{D}_t} \|x - x'\| > \delta_{\min}\right]$$

Where $\tau_{\text{util}}$ is set dynamically to the 70th percentile of recent acquisition values.

**Reproducibility certificate** (enables deterministic re-execution):

$$c_{\text{repro}} = \text{SHA256}(\text{conda\_env}) \| \text{SHA256}(\text{docker\_image}) \| s \| \theta$$

Where $s$ is the committed random seed and $\theta$ is the complete parameter vector — both committed before execution begins.

### 6.2 Execution Gate

If $\neg \text{valid}(x, m)$: diagnose which certificate failed → generate repair suggestions → return to council. The experiment does not run. Not a warning. Not a soft suggestion. An architectural gate.

---

## 7. Multi-Fidelity Bayesian Optimization

### 7.1 Cross-Fidelity GP

$$f^{(\ell)}(x) = \rho_\ell \cdot f^{(\ell-1)}(x) + \delta^{(\ell)}(x)$$

Where $\rho_\ell$ is the learned cross-fidelity correlation parameter and $\delta^{(\ell)}$ is the fidelity-specific deviation. This allows cheap simulation data to inform expensive wet-lab experiment selection — the key cost reduction mechanism.

**GP posterior update after observation $(x_{\text{new}}, m_{\text{new}}, y_{\text{new}})$:**

$$\mu_{t+1}(x) = \mu_t(x) + k(x, x_{\text{new}}) \cdot \left[k(x_{\text{new}}, x_{\text{new}}) + \sigma^2(x_{\text{new}})\right]^{-1} (y_{\text{new}} - \mu_t(x_{\text{new}}))$$

### 7.2 Acquisition Functions

**UCB with theoretical regret guarantee:**

$$\alpha_{\text{UCB}}(x, m) = \mu_t(x, m) + \beta_t^{1/2} \cdot \sigma_t(x, m)$$

$$\beta_t = 2\log\!\left(|\mathcal{X}| \cdot t^2 \pi^2 / 6\delta\right) \quad \text{(from Srinivas et al., sublinear regret)}$$

**Multi-fidelity Expected Improvement (information per dollar):**

$$\text{MF-EI}(x, m) = \frac{\text{EI}(x, m)}{\text{Cost}(x, m)}$$

**Thompson sampling for budget allocation:**

$$\pi^*_{\text{budget}}(e_j) = \frac{\tilde{f}(e_j) \cdot \mathbf{1}[B \geq \text{Cost}(e_j)]}{\sum_k \tilde{f}(e_k) \cdot \mathbf{1}[B \geq \text{Cost}(e_k)]}, \quad \tilde{f} \sim \text{GP}_t$$

---

## 8. Self-Reasoning & Meta-Learning

### 8.1 Epistemic State Tensor

Each agent $i$ maintains:

$$\Psi_i^t = (\hat{\mu}_i^t, \hat{\Sigma}_i^t, \mathcal{K}_i^t, \mathcal{R}_i^t)$$

**Kalman-filter belief update:**

$$K_{\text{gain}} = \hat{\Sigma}_i^t \cdot [\hat{\Sigma}_i^t + R_{\text{noise}}]^{-1}$$

$$\hat{\mu}_i^{t+1} = \hat{\mu}_i^t + K_{\text{gain}} \cdot (y_t - \hat{\mu}_i^t)$$

$$\hat{\Sigma}_i^{t+1} = (I - K_{\text{gain}}) \cdot \hat{\Sigma}_i^t$$

### 8.2 MAML Bi-Level Meta-Learning

**Inner loop (domain-specific adaptation):**

$$\theta'_i = \theta_{\text{inner}} - \beta \nabla_{\theta_{\text{inner}}} \mathcal{L}_{\text{task}}(\theta_{\text{inner}}, \mathcal{D}_{\text{domain}})$$

**Outer loop (cross-domain meta-update):**

$$\theta_{\text{meta}} \leftarrow \theta_{\text{meta}} - \alpha \nabla_{\theta_{\text{meta}}} \sum_{\text{domain}_j} \mathcal{L}_{\text{task}}(\theta'_{i,j})$$

After training across drug discovery, materials, and climate domains, the system adapts to a new domain (e.g., agricultural chemistry) with far fewer examples — the meta-learned initialization $\theta_{\text{meta}}$ encodes what a good scientific hypothesis generation policy looks like across domains.

### 8.3 Elo-Weighted Bayesian Model Averaging

**Elo credibility update after prediction-verification cycle:**

$$w_i^{(t+1)} = w_i^{(t)} \cdot \exp\!\left(\eta_w \cdot \frac{\text{TP}_i - \text{FP}_i}{\text{TP}_i + \text{FP}_i + 1}\right)$$

**Council consensus:**

$$P(h^* \mid \mathcal{D}, \text{debate}) = \frac{\sum_i w_i \cdot P(h \mid \mathcal{D}_i)}{\sum_i w_i}$$

**Elo hypothesis matchup** (3 debate rounds):

$$E_a = \frac{1}{1 + 10^{(r_b - r_a)/400}}, \quad r_a^{\text{new}} = r_a + K(S_a - E_a)$$

Where $S_a \in \{0, 0.5, 1\}$ based on experimental outcome.

---

## 9. Evidence Graph

### 9.1 Schema

The Evidence Graph is the central data structure enabling reproducibility, provenance, and automated publication. All nodes and edges are SHA-256 hashed and cryptographically signed at creation time. The graph is append-only — retroactive modification is architecturally impossible.

**Vertex types:** `Claim`, `Hypothesis`, `Experiment`, `Observation`, `Parameter`, `Code`, `Instrument`, `Agent`, `PreRegPlan` (immutable after commit)

**Edge types:** `tested_by`, `produces`, `supports` (weight: e-value), `contradicts` (weight: e-value), `parameterized`, `executed_by`, `run_on`, `performed_by`, `preregistered`, `cites`

### 9.2 Cryptographic Chain

$$\text{node\_hash}(v) = \text{SHA256}(\text{content}(v) \| \text{timestamp}(v) \| \text{parent\_hash}(v))$$

Every node's hash includes its parent's hash — creating a Merkle-tree-like chain that makes retroactive modification computationally infeasible. This provides scientific custody chain from hypothesis to publication.

---

## 10. Convergence Theorems

### 10.1 Theorem 1: Sublinear Regret of PIHSN-GP-UCB

**Theorem.** Let $f: \mathcal{M}_\phi \rightarrow \mathbb{R}$ be continuous with bounded RKHS norm $\|f\|_k \leq B$. The cumulative regret of PIHSN-GP-UCB satisfies:

$$R_T = \sum_{t=1}^T [f(x^*) - f(x_t)] \leq \mathcal{O}\!\left(\sqrt{T \cdot \gamma_T \cdot \log T}\right)$$

**Proof sketch.** (1) The physics manifold $\mathcal{M}_\phi$ is compact (each constraint defines a closed bounded set; finite intersection remains compact). (2) By Srinivas et al. (2010), GP-UCB achieves $\mathcal{O}(\sqrt{T \gamma_T})$ regret on compact domains. (3) SGLD with manifold projection converges to the posterior $p(z \mid \mathcal{D}_t)$ restricted to $\mathcal{M}_\phi$ by log-Sobolev inequality with mixing time $\mathcal{O}(d_{\text{eff}}/\varepsilon^2)$. (4) Combining: PIHSN-GP-UCB inherits the GP-UCB bound on the constrained space. $\square$

### 10.2 Theorem 2: Anytime Validity of Sequential E-Values

**Theorem.** Let $\{e_t\}$ be the POPPER e-value sequence. The product process $E_T = \prod_{t=1}^T e_t$ satisfies:

$$P\!\left(\exists T \geq 1: E_T \geq 1/\alpha \mid H_0\right) \leq \alpha$$

**Proof.** Under $H_0$, $\mathbb{E}[e_t \mid \mathcal{F}_{t-1}] \leq 1$ (definition of e-value). Therefore $E_T$ is a non-negative supermartingale. By Ville's inequality: $P(\sup_T E_T \geq 1/\alpha) \leq \alpha \cdot \mathbb{E}[E_0] = \alpha$. This holds at **any** stopping time $T$ — the test is valid regardless of when the autonomous loop terminates. $\square$

### 10.3 Theorem 3: MAML Convergence

**Theorem.** Under $L$-smoothness and bounded gradients, the MAML outer loop satisfies:

$$\|\nabla_{\theta_{\text{meta}}} \mathcal{L}_{\text{meta}}(\theta_{\text{meta}}^T)\|^2 \leq \mathcal{O}(1/T)$$

with step size $\alpha = \mathcal{O}(1/\sqrt{T})$. Proof follows from standard smooth non-convex gradient descent convergence. $\square$

---

## 11. Novelty Claims

The following represent genuine architectural novelty — features not present in any published or deployed autonomous scientific discovery system:

**NC1: Ethics as Deliberation.** No prior system (Coscientist, LabOS, CoSA, ASDL, ASDP, AI Scientist, Google AI Co-Scientist, A-Lab) includes a deliberative Ethics Agent in the discovery loop. All prior work implements ethics as a static filter. Kaimei's agent reasons about context-dependent harm with structured assessments and unconditional veto.

**NC2: Pre-Registered Analysis Plans.** Committing statistical analysis plans to an immutable Evidence Graph node before data is generated has never been implemented in any autonomous discovery system. This prevents systematic p-hacking by the loop.

**NC3: Legal/IP Agent.** Entirely absent from all seven prior proposals. Essential for a commercial SaaS product serving SMEs who need to know who owns their discoveries.

**NC4: Reproducibility Auditor as Distinct Role.** Statistical validity and reproducibility are orthogonal failure modes. No prior system separates them architecturally.

**NC5: Mandatory Auto-Populated Limitations.** Limitations section generated non-overridably from Evidence Graph flagged nodes. Autonomous papers without honest limitations are a scientific integrity problem.

**NC6: Devil's Advocate with Inverted Loss and Different Checkpoint.** Structural diversity between the Researcher and Skeptic is the architectural defense against sycophancy collapse. All prior multi-agent systems use agents from the same base model.

**NC7: PIHSN + PCEC Integration.** The combination of physics-manifold constrained hypothesis generation with proof-carrying experiment certification has not been implemented in any prior system.

**NC8: Cryptographic Evidence Graph.** Cryptographically signed, append-only evidence trail from hypothesis to publication. Provides verifiable scientific custody chain.

---

## 12. Ablation Study Design

All ablations: 5 random seeds, scaffold/temporal splits, 95% CIs, paired t-test for significance.

| Stage | Variant Tested                                      | Metric                                  | Acceptance Threshold           | Fast-Fail Criterion                      |
| ----- | --------------------------------------------------- | --------------------------------------- | ------------------------------ | ---------------------------------------- |
| 0     | Baselines (random, BoTorch, Coscientist)            | QED×SA at N={50,100,250,500}            | —                              | —                                        |
| 1     | PIHSN vs. unconstrained                             | Valid candidates per 100 samples        | ≥3× improvement                | <3×: pivot to data-driven constraints    |
| 2     | Council (3-agent, 11-agent) vs. single LLM          | Elo correlation with expert ≥0.7        | ≥2× hypothesis quality         | <2×: council overhead unjustified        |
| 3     | Full PCEC vs. no certs vs. partial                  | Safety violations on adversarial set    | Zero safety violations         | Any violation: halt physical deployment  |
| 4     | Pre-reg+e-values vs. p-values vs. no stat oversight | FDR over 200 null-hypothesis iterations | FDR ≤0.05 at any stopping time | FDR >0.08: statistical framework invalid |
| 5     | Multi-fidelity vs. single fidelity                  | Cost-to-target ($USD)                   | ≥5× cost reduction             | <3×: insufficient for value prop         |
| 6     | MAML vs. no meta-learning                           | Sample efficiency on new domain         | ≥2× efficiency gain            | <1.5×: defer meta-learning indefinitely  |

---

## 13. Implementation Roadmap

**Phase 0 — Foundation (Months 1–3)**
PIHSN core (GVAE + physics constraints + SGLD) for drug discovery. Typed Experiment DSL + Certificate Agent. 3-agent council (Researcher + Devil's Advocate + Statistician). Evidence Graph with cryptographic hashing. LaTeX generator. Benchmark: ZINC250k, Matbench.
_Deliverable: Working virtual-only closed loop, 1 domain._

**Phase 1 — Safety & Governance (Months 4–5)**
Ethics Agent (IRB-grade). Legal/IP Agent. Pre-registered analysis plans (immutable). Sequential e-value tester. Reproducibility Auditor. Science Writer with mandatory limitations. Simulated peer review (3 reviewer personas).
_Deliverable: Full 11-agent council, all safety gates active._

**Phase 2 — Physical Integration (Months 6–8)**
Emerald Cloud Lab API connector (Autoprotocol). Multi-fidelity GP (cross-fidelity kernel). Multi-provider abstraction layer. Real-time anomaly detection. Human-on-call for high-risk tier.
_Deliverable: First physical closed loop._

**Phase 3 — Scale & Self-Improvement (Months 9–12)**
MAML bi-level meta-learning. Materials science + climate domains. Dynamic LoRA agent spawning. Multi-tenant SaaS + billing. PPO meta-RL (only after ablation Stage 6 confirms benefit).
_Deliverable: Multi-domain SaaS, public academic tier._

**Phase 4 — Democratization (Months 13–18)**
Citizen scientist tier (free, virtual-only). Marketplace of experiment templates. First peer-reviewed publication of AI-discovered compound under Kaimei authorship.
_Deliverable: Public product launch, validated external discovery._

---

## 14. Risk Register

| Risk                           | P   | S   | Mitigation                                                                    |
| ------------------------------ | --- | --- | ----------------------------------------------------------------------------- |
| GVAE training instability      | H   | M   | Fallback: RDKit enumeration + physics filter for MVP; GVAE as Phase 2 upgrade |
| Ethics agent over-conservatism | M   | H   | Tunable threshold per domain; ablation stage 3; human override API            |
| Meta-RL divergence             | M   | M   | PPO clip $\varepsilon=0.2$; defer to Phase 3; fallback to fixed BO            |
| LLM hallucination in protocols | H   | C   | PCEC + typed DSL catch before execution — primary defense                     |
| Pre-registration circumvention | L   | C   | Cryptographic hash + append-only graph — technically impossible               |
| Devil's advocate sycophancy    | M   | M   | Different base checkpoint + inverted loss; monitor disagreement rate          |
| Cloud lab API unavailability   | M   | H   | Multi-provider abstraction; virtual-only tier unaffected                      |
| Spurious publication           | M   | C   | Pre-registration + e-values + Reproducibility Auditor — triple protection     |
| FDA regulatory pathway (drugs) | M   | H   | Start materials (no FDA); drug discovery labeled research-use-only            |
| IP ownership disputes          | M   | H   | Legal/IP Agent + explicit ToS: user owns discoveries from user hypotheses     |
| Data leakage in surrogates     | M   | H   | Temporal split mandatory; scaffold split for molecular benchmarks             |

P: H/M/L (High/Medium/Low probability), S: C/H/M/L (Critical/High/Medium/Low severity)

---

## 15. Complete Discovery Loop (Pseudocode)

```python
class KaimeiDiscoveryLoop:
    def run(self, goal: str, budget: float, tau_breakthrough: float = 0.90):
        # Initialize
        K = council.curator.retrieve(goal)  # RAG from literature
        trajectory = ResearchTrajectory(domain=config.domain, goal=goal)

        while budget > 0:
            # 1. Physics-manifold sampling
            candidates = pihsn.langevin_sample(n=30, gp=gp)

            # 2. Self-critique (4-stage: logic, physics, novelty, impact)
            candidates = [rmre.critique(h, K) for h in candidates]
            candidates = [h for h in candidates if h is not None]
            if not candidates:
                pihsn.expand_manifold_radius(1.5); continue

            # 3. Council adversarial debate (Elo + BMA consensus)
            h_star = council.debate(candidates, rounds=3)

            # 4. Pre-registration (IMMUTABLE — committed before any data)
            stat_plan = statistician.preregister(h_star)
            evidence.commit_preregistration(stat_plan)

            # 5. Certification (all 6 certificates required)
            e_proposed = experimentalist.design(h_star, gp)
            cert = certificate_agent.certify(e_proposed)
            if not cert.is_valid:
                h_repaired = council.repair(h_star, cert); continue

            # 6. Fidelity selection + execution
            fidelity = select_fidelity(e_proposed, budget)
            outcome = gym.execute(e_proposed, fidelity)
            budget -= gym.cost(e_proposed, fidelity)

            # 7. Bayesian GP update
            gp.update(e_proposed, fidelity, outcome)

            # 8. Sequential e-value falsification (POPPER)
            if popper.should_reject(h_star, stat_plan, outcome):
                trajectory.failed_hypotheses.append(h_star)
                trajectory.flagged_nodes.append(
                    f"POPPER rejection: {h_star.id} at iter {t}")
                continue

            # 9. Meta-learning update
            maml.outer_update(trajectory)
            council.update_elo_weights(h_star, outcome)

            # 10. Evidence graph (cryptographically signed)
            evidence.append(h_star, e_proposed, fidelity, outcome, cert, stat_plan)

            # 11. Breakthrough check
            if compute_impact(h_star, outcome) > tau_breakthrough:
                break

        # Publication (only if reproducibility audit passes)
        audit = repro_auditor.audit(h_best, evidence)
        if not audit.reproduced:
            trajectory.flagged_nodes.append(f"Repro audit failure: {audit.delta}")

        paper = writer.write(trajectory, K, evidence)  # Includes mandatory limitations
        paper = peer_review_loop(paper, n_reviewers=3)
        return h_best, paper
```

---

## Appendix: LaTeX Template (Auto-Generated)

```latex
\documentclass[11pt]{article}
\usepackage{amsmath,amssymb,graphicx,hyperref,algorithm,algorithmic,booktabs}

\title{[AUTO: hypothesis_title]}
\author{Kaimei Autonomous Discovery System\\
\small Agent Council v[version] $\cdot$ Evidence Graph: [G_E.id]}

\begin{abstract}
[AUTO: summarize(G_E.top_findings(k=3))]
\end{abstract}

\section{Introduction}
[AUTO: RAG retrieval + motivation]

\section{Methods}
\textit{Pre-registered analysis plan committed [timestamp],
hash: [hash]. Available at: [G_E.archive\_url].}
Sequential e-value testing used for hypothesis validation,
providing anytime-valid type-I error control at $\alpha = 0.05$.

\section{Results}
[AUTO: report\_with\_CI(G_E.all\_observations)]

\section{Discussion}
[AUTO: causal\_interpretation(G_E.validated\_hypotheses)]

\section{Limitations}
%% MANDATORY — auto-populated from Evidence Graph flagged nodes
%% This section cannot be empty or removed by any agent
[AUTO: populate\_from\_flagged\_nodes(G_E)]

\section{Data \& Code Availability}
All data and code available at \url{[G_E.archive\_url]} and \url{[G_E.github\_url]}.

\bibliographystyle{nature}
\bibliography{[AUTO: semantic\_scholar\_bibtex]}
\end{document}
```

---

This is the complete Kaimei specification. Every formula is grounded in prior work or explicitly labeled as a hypothesis requiring validation. The $10^{45}$ efficiency figure does not appear anywhere — empirical efficiency claims will be made only after ablation stages 1–2 complete.

The three load-bearing novelties that make this a defensible academic and commercial contribution are: **pre-registered analysis plans in autonomous loops** (NC2), **Ethics as deliberation with unconditional veto** (NC1), and **Legal/IP Agent for commercial viability** (NC3). Everything else — the physics manifold, the proof-carrying certificates, the MAML meta-learning — builds the discovery engine that these governance mechanisms make safe enough to deploy.
