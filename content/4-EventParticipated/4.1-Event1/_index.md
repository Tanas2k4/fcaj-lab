---
title: "Event 1"
date: 2026-05-23
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy it verbatim** into your report, including this warning.
{{% /notice %}}

# Summary Report: "AWS Vietnam Community Day 2026"

### Event Objectives

- Explore the latest technology trends in Generative AI (GenAI), Multi-Agent systems, and AWS cloud infrastructure optimization.
- Gain practical insights and learn solution design experiences from leading engineers and experts in Vietnam.
- Connect with the technology community, share soft skills, teamwork lessons, and career orientation in the AI era.

### Speakers & Topics

- **Tinh Truong** – Platform Engineer at GoTymeX
  * *Topic:* Context Is Everything: Making AI Actually Work for You
- **Pham Ng Hai Anh** – G-AsiaPacific Vietnam, AWS Community Builder
  * *Topic:* Friendly AI Assistant w/ Amazon Q in QuickSight
- **Nguyen Tuan Thinh** – DevOps Engineer, First Cloud AI Journey
  * *Topic:* From Edge to Origin: CloudFront as Your Foundation
- **Team VIB** – LotusHacks 2026
  * *Topic:* 36 hrs with LotusHacks: Building UTMorpho from Idea to Reality
- **Duc Dao** – Solution Architect at Cloud Kinetics
  * *Topic:* Non-Determinism of "Deterministic" LLM Settings
- **Vy Lam** – Senior Business Systems Analyst at VPBank
  * *Topic:* Enterprise-Grade Multi-Agent System: The Case of Startup Credit Scoring

### Key Highlights

#### 1. Context Management in AI Applications (Speaker Tinh Truong)
- **The Importance of Context**: AI functions effectively only when provided with complete context information. Context bridges the gap and minimizes hallucinations of LLMs.
- **Optimization Strategy**: Prompt structuring, context window size management, and matching retrieval strategies to ensure the model yields the most accurate output.

#### 2. AI Assistant with Amazon Q in QuickSight (Speaker Pham Ng Hai Anh)
- **Integrating GenAI into Business Intelligence**: Utilizing Amazon Q in QuickSight to automate data analysis and automatically generate dashboards using natural language queries.
- **Productivity Boost**: Shortens time-to-insight for businesses and facilitates quick decisions through direct natural language interaction with data.

#### 3. Infrastructure Optimization with Amazon CloudFront (Speaker Nguyen Tuan Thinh)
- **EC2 CPU Offloading**: Using CloudFront to handle data compression (reducing transfer payloads, saving up to 82% CPU load for the origin EC2 servers) and TLS handshake processing.
- **Robust Security at Edge**: Leveraging AWS's global Edge network to mitigate DDoS attacks and filter malicious traffic directly at the border before it reaches the origin servers.

#### 4. 36-Hour Hackathon Journey at LotusHacks: Building UTMorpho (Team VIB)
- **UTMorpho Project**: Building an AI Agent to generate and directly edit user interfaces on an interactive visual canvas (WYSIWYG editor) from natural language descriptions, preventing design drift from repeated re-prompts.
- **Hackathon Lessons**: The most practical ideas arise from daily operational pain points. Under tight time pressure (36 consecutive hours), coordination and chemistry within the team matter more than individual skills.

#### 5. LLM Non-Determinism in Real-world Applications (Speaker Duc Dao)
- **Non-Determinism Phenomenon**: Analyzing why LLMs produce variable outputs for identical inputs even with temperature configured to 0 (caused by float calculation errors on GPUs and concurrency).
- **Control Strategy**: Designing system architectures and guardrails (e.g., structured output parsing) to mitigate non-deterministic behavior in enterprise-grade applications requiring strict consistency.

#### 6. Enterprise-Grade Multi-Agent System for Credit Scoring (Speaker Vy Lam)
- **Startup Credit Approval Challenge**: Overcoming the information asymmetry between traditional banking governance standards and the dynamic, volatile nature of startup data.
- **Multi-Agent Architecture**: Modeling the virtual credit committee process into specialized AI agents (Financial Agent, Compliance Agent, Risk Agent, etc.).
- **Business Value**: Automating complex analysis workflows, saving up to 95% of operational time and costs while strictly maintaining compliance, security, and governance standards.

### Lessons Gained

#### AI Application Design Mindset
- **Business-First Approach**: AI applications must solve real-world business challenges (e.g., credit committee approval or automated BI analytics) rather than adopting technology for technology's sake.
- **Multi-Agent Paradigm**: Deconstructing large systems into dedicated AI agents with clear responsibilities and boundaries to handle complexity systematically.

#### Cloud & AI Architecture
- **Leveraging the Edge**: Maximizing CDN (Amazon CloudFront) capabilities to optimize content delivery and establish a robust perimeter defense shield.
- **Enforcing Consistency**: Structuring large language model output mechanisms to guarantee reliable and predictable application behaviors.

#### Soft Skills & Teamwork
- **Critical Communication**: Smooth collaboration and transparent cross-functional alignment determine project success more than isolated individual efforts.

### Key Takeaways

* **Business Aspect**: Implementing a Multi-Agent model automates startup credit analysis and reduces processing time by up to 95%.
* **Technical Aspect**: Understanding LLM non-determinism and optimizing Context to maximize AI prompt performance.
* **Infrastructure Aspect**: Deploying CloudFront at Edge to reduce data transfer fees, offload origin EC2 CPU usage by up to 82%, and bolster DDoS protection.

### Applying to Work

- Applying context optimization techniques to improve accuracy for chatbots and AI pipelines in current workflows.
- Implementing Amazon CloudFront caching and edge security rules to optimize web server delivery and protection.
- Researching Multi-Agent frameworks to automate complex, multi-step business approval processes.

### Event Experience

Attending **AWS Vietnam Community Day 2026** was a highly valuable experience, offering a comprehensive look from theoretical design to enterprise-grade AI and Cloud deployment:

#### Learning from Industry Experts
- Speakers from VPBank, GoTymeX, and Cloud Kinetics shared highly specialized, practical insights from production-grade architectures.

#### Exploring Advanced Solutions
- Hands-on look at next-gen BI via Amazon Q in QuickSight, investigating LLM non-determinism under zero-temperature configurations, and studying VPBank's Multi-Agent architecture.

#### Community Networking
- Discussing directly with AWS Community Builders and industry peers, broadening professional networks, and observing standard engineering practices.

#### Key Takeaway
- AI and Cloud are mutually beneficial; a great AI system requires an optimized, secure-at-edge cloud infrastructure and resilient software architectures to manage the uncertainty of LLMs.

#### Some event photos

![Ms. Ngoc Uyen speaking](/images/meetup-2305.jpg)
*Figure 1: Ms. Ngoc Uyen sharing her insights at the session*

![Winning the Lucky Draw](/images/meetup-2305-3.jpg)
*Figure 2: I was fortunate enough to win the Lucky Draw prize at the event*

![AWS Vietnam Community Day 2026](/images/meetup-2305-2.jpg)
*Figure 3: Overview of AWS Vietnam Community Day 2026 event*

> Overall, the event not only provided technical knowledge but also helped me reshape my thinking about application design, system modernization, and cross-team collaboration.
