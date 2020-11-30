# Handling Incidents

Our solution provides a **framework** to face incidents that can eventually happen. Our framework covers the two stages that appear during an incident:

- [Dealing with the incident](#dealing-with-the-incident),
- [Documenting the incident](#documenting-the-incident).

The purpose of our framework is:
- To **maximize the time while the environment is working**,
- to **minimize the impact** on the customer,
- to **reduce the time needed to repair the system**,
- to **foster transparency**: ensure that the customer, the staff, the stakeholders, and the community are aware of happened incidents and our commitment to their solution.

You will find a list of [past incidents, here](./history).


## Dealing With the Incident

Incidents will be categorized by severity. We'll apply the following category levels:

- **P0**. The infrastructure is **out of control**. The access to the system is lost,
- **P1**. **Security issues**,
- **P2**. **Data loss**,
- **P3**. Customers **can not access the service**,
- **P4**. One primary function is **not working according to SLO**,
- **P5**. Some additional functionality is not working as desired,
- **P6**. There is some degradation of the service,

Incidents with severity **P0** to **P4** will be a high priority for all the departments affected, and once they're solved, a postmortem will document them. Incidents **P5** and **P6** can be considered as minor incidents and solved like any other regular issue.

Dealing with an incident will require:
- To perform an initial **triage**: Once we're aware of an incident, it's needed to assign a category according to its severity, assign a team, and a strategy.
- To work to **restore the normality**.
- To **investigate deeper** about causes, effects, and impacts.

A severe incident uses to involve a chain of causes, alerts, problems, uncertainties, etcetera, along the time, so all the three processes above may happen at the same time. All the resources involved in each process must share their knowledge with others.

To facilitate the elaboration of the postmortem that will document the incident, it's needed that the team:
- makes sure **no information is lost** while recovering the system (e.g., logs are saved),
- makes sure all the **procedures are registered with their timestamps**.

There will be a role to:
- lead the teams solving and mitigating the incident,
- follow the whole incident, and facilitate communication,
- represent the interest of the customer,
- make sure the framework is followed,
- ensure the customer is well informed according to the available information about expected times and impacts,
- confirm the incident is solved, and the customer agrees.


## Documenting the Incident

Once the incident is solved, or once this process can start, it is needed to document what happened.

The principles that will guide this process will be:
- **Transparency**: make sure all people impacted by the incident, and product stakeholders, are at least informed about the postmortem.
- **Blameless analysis**: the postmortem is focused on causes and consequences and understands why each decision was made.
- **Opportunity to enhance**: The postmortem will let the team and stakeholders know which things failed, what can be improved, and offer a plan to enhance processes and the product itself.
- **Dig deeper**: root causes use to be deeper. Serious consequences use to be caused by a chain of failures, so it's needed to describe all of them.
- **Details matter**: make sure you identify them from logs and interviews.
- **Be diligent**. Documenting an incident is not about solving issues. Identify them so others will be able to fix them later.
- **Recognise uncertainties and unknowns**. Identify all of them.
![](https://miro.medium.com/max/1652/1*Bg0Dbo8wrqLf1e_nQpoMpA.jpeg)
(source [Knowns vs Unknowns, by Aaron Batalion @ LivingSocial](https://medium.com/lightspeed-venture-partners/knowns-vs-unknowns-78b0da5ca887))

Our framework proposes the following sections for our post-mortems:
- [TL;DR](#tl-dr)
- [Description of the Incident](#description-of-the-incident)
- [Consequences. Negative Impact](#consequences-negative-impact)
- [Risk Analysis](#risk-analysis)
- [Action Plan](#action-plan)
- [Addendum. Timeline](#addendum-timeline)
- [Addendum: Interview Minutes](#addendum-interview-minutes)

You can use this [postmortem template](./template.md).


### TL;DR

Summary for the reader. It should include one paragraph acting as a summary for each of the three main sections of the postmortem: description, consequences, and action plan.

It should also explain when the system started to malfunction, when it was first detected and when the service was restored.

### Description of the Incident

A clear description of what happened and in which order. Focus on the cause-effect principle.

It is not mandatory to focus on exact times; there will be a dedicated addendum with an accurate timeline.

### Consequences. Negative Impact

This section will help to understand who and why suffered any consequence of the incident. It's important to reflect all kinds of negative impacts, no matter where they happened, e.g., customers, employees, company, or product reputation.

Measure every kind of impact, e.g., money that the customer lost, extra hours spent by the staff, retweets, lost deals, etcetera.

### Risk Analysis

Explain the risk's initial consideration and evaluate if the previous assumptions and estimations were made correctly.

Explain if the estimation of the risk changed in any way as a consequence of the incident.

_(Note: Remember that the "risk" measures the possible consequences and the probabilities of them to happen. The probabilities of a consequence to happen depends on the chances of its causes to exist and the probability of the effect once given the cause.)_

### Action Plan

This section explains what was done and what should be done to achieve:
- **Resolution** of the found problems.
- **Mitigation** of the consequences that can not be avoided.
- **Prevention** of further incidents and outages.
- **Monitoring** of the system, which should raise notifications when operating beyond defined thresholds, and alerts when malfunctioning.
- **Resilience**. The system should implement processes to automatically self recover from malfunctioning states.
- **Knowledge sharing**. Plan to ensure that the whole stack is aware of what happened and how to deal with and avoid the issues found. It should also include revising existent processes, checklists, and protocols to guarantee they are adapted to the new experience.

### Addendum. Timeline

A detailed list of events in chronological order. It will support the description of the incident and its consequences as described above.

This section will help to understand what happened and when, how the information appeared, and when the people reacted.

Find below some of the events that should be logged:
- **signals** and **alerts** that the system raised, and if they were acknowledged,
- **system failures** and their **criticality**,
- measurable **consequences**, if it elapsed some time between the failure and the consequence,
- **actions** that were made, explaining if they were automatically done by the system or by the staff.

### Addendum: Interview Minutes

The minutes of the interviews can also help to extract new conclusions in further readings. It's essential to interview all the people involved in the incident
- the **staff** that fought against the incident and those in charge of solving the issues,
- the **people from business**, marketing, etcetera will spotlight the impact on other fields: costs, reputation, confidence...
- the **people impacted** by the incident, also customers, which will help you to enhance your communication.
