# Hackathon Reflection — Week 5 Diagnostics

**Pod:** Oil & Gas
**Dataset:** Mystery Ops (`Mystery_Ops.csv`)

## What I Built

Over this hackathon I worked through a full diagnostics investigation on the Mystery Ops dataset — daily production records across four depots and 13 machines for calendar year 2026. The deliverables were a technical notebook (data profiling → anomaly detection → root-cause analysis → visualization) and a 2-page executive report translating the findings for a non-technical audience.

The headline finding: one machine, `NBI-P03` at the Nairobi depot, was responsible for roughly 86% of all fleet-wide throughput loss for the year, driven by a missed-maintenance pattern that started in February and was never caught.

## Technical Challenges

- **[Fill in: any environment/setup friction you personally hit — e.g. package installs, Colab quirks]**
- **Isolating signal from noise:** the univariate histogram alone only hinted at a problem (a bimodal distribution); it took layering the anomaly detection (box plot by machine), the drill-down (depot → machine → month), and the Pareto analysis together before the root cause became unambiguous. No single technique was conclusive on its own.
- **Ruling things out, not just in:** part of the exercise was resisting the temptation to stop at the first plausible driver. Checking temperature and voltage correlations (and finding both negligible) was as important to the final conclusion as finding the maintenance-flag correlation.
- **Writing for two audiences:** the notebook and the report needed genuinely different vocabularies — the same "correlation coefficient of -0.85" in the notebook became "we checked whether weather or power supply explained this — neither did" in the report. Translating a quantitative finding into a plain-English recommendation without losing precision was harder than expected.

## What I Learned

- A drill-down + Pareto + correlation combination is a reliable pattern for root-cause work: drill-down localizes *where*, Pareto quantifies *how much*, and correlation helps rule candidate drivers *in or out* rather than just confirming a hunch.
- Anomalies are more convincing when shown two ways — categorically (this one asset is different) and temporally (it became different at a specific point in time). Either alone is suggestive; together they're close to proof.
- A good executive report doesn't summarize the whole analysis — it picks the two or three numbers that carry the argument and cuts everything else.

## What I'd Do Differently Next Time

- **[Fill in: e.g. start the drill-down earlier, spend less time on univariate plots, check correlations before/after anomaly detection, etc.]**
- Build the "loss" baseline calculation earlier in the process — it ended up being the backbone of both the Pareto analysis and the report's headline numbers, and defining it sooner would have saved some rework.

## Acknowledgments

**[Fill in: pod partners, mentors, or resources that helped — see companion `pod_feedback.md` for collaboration-specific notes]**
