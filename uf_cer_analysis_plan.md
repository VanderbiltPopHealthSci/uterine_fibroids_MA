# Analysis plan: Uterine fibroids follow- up treatment meta-analysis

### Chris Fonnesbeck
**22 December 2015**

Our goal is to estimate the probabilities of requiring one of a suite of candidate follow-up treatments following randomization to a given initial treatment for uterine fibroids. Specifically, we are interested in estimating:

$$Pr(I_2|I_1 =i,T=t)$$

where $I_1$ is an initial intervention, which take specific values $i = 1, 2, \ldots , K$ for each of $K$ candidate intervention types, $I_2$ is the followup intervention that also may take any of the same values of $i$, and $T$ is followup time in months, which will generally be either 6 or 12 months.

Our current set of candidate interventions include:

- Myomectomy
- Hysterectomy
- Ablation
- UAE
- Magnetic resonance imaging-guided high-intensity focused ultrasound (MRIgFUS) 
- Ablation +/- hysteroscopic myomectomy
- No intervention

Rather than model each conditional probability independently, we will instead model the outcomes for a treatment arm as a multinomial random variable. That is,

$$\{X_{I_2} \} ∼ \text{Multinomial}(N_{I_1}=i, \{\pi_i\})$$

where $\{X_{I_2}\}$ is the vector of outcomes corresponding to each of the possible followup interventions listed above, $N_{I_1}=i$ is the number of women randomized to the initial intervention i, and $\{\pi_i\}$ is a vector of conditional transition probabilities corresponding to $Pr(I_2|I_1 = i, T = t)$, as specified above. The multinomial distribution is a multivariate generalization of the categorical distribution, which is what the above simplifies to when modeling the outcome for a single patient. The multivariate formulation allows us to model study-arm-specific outcomes, incorporating covariates that are specific to that arm or study.
       
The quantities of interest are the vectors of transition probabilities $\{\pi_i\}$ corresponding to each of the initial candidate interventions. A naive approach to modeling these is to assign a vague Dirichlet prior distribution to each set, and perform Bayesian inference using the multinomial likelihood, with which the Dirichlet is conjugate, to yield posterior estimates for each probability. However, there may be additional information with which to model these probabilities, which may include:

- followup time for each study
- arm-specific demographic covariates (e.g. race, mean age) 
- study-specific random effects

hence, a given transition probability $\pi_{ijk}$ – the probability of transitioning from initial intervention $i$ to followup intervention $j$ in study $k$ – may be modeled as:

$$\text{logit}(\pi_{ijk})= \theta_{ij} + X_k \beta_{ij} + \epsilon_k$$

where $\theta_{ij}$ is a baseline transition probability (on the logit scale), $X_k$ a matrix of study(-arm)-specific covariates, $\beta_{ij}$ the corresponding coefficients, and $\epsilon_k$ a mean-zero random effect for study k. We will initially consider (1) follow-up time and (2) mean/median age as covariates.
 
An attractive benefit to using Bayesian inference to estimate this model is that it is easy to generate predictions from the model, via the posterior predictive distribution. For example, we could estimate the distribution of the expected proportion of women requiring a particular followup intervention; this estimate would factor in both the residual uncertainty in the transition probability estimates, as well as the sampling uncertainty of the intervention.
    