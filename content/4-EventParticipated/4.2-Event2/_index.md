---
title: "Event 2"
date: 2026-05-23
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Event Report: “FCAJ Community Day - May 2026 Edition”

### Objectives of the Event

* Update macro trends and position the Vietnamese IT market in the era of rapidly advancing AI.
* Share methodologies for designing Context-Optimized Prompt structures and controlling Large Language Model (LLM) Randomness.
* Introduce enterprise data analytics assistant solutions using Amazon Q Business (QuickSight/Q Desktop) integrated with MCP servers.
* Share practical hands-on experiences from Hackathons and design principles for Enterprise-grade Multi-Agent systems applied in the Banking and Finance sector.

### Speakers

* **Mr. Nguyen Gia Hung** - Solutions Architect at AWS Vietnam & Founder of FCAJ (Sharing macro market directions).
* **Mr. Tinh Truong** - Platform Engineer at Gothamic X (Sharing Context Optimization Techniques and LLM Randomness).
* **Mr. Hai Anh** - Solutions Architect at Pacific Vietnam (Sharing Amazon Q Business & MCP).
* **Mr. Nguyen Han Thinh** - DevOps Engineer (Sharing Flat-rate Pricing mechanisms and advanced security features of Amazon CloudFront).
* **Uyen, Mach & Ms. Thao** - Hackathon Winning Team (Sharing their 36-hour journey developing the UTMorpho project).
* **Final Speaker (FinTech Engineer)** - FinTech Solutions Advisor at VPBank (Sharing Multi-Agent architectures applied in banking).

### Key Highlights

#### 1. IT Market Positioning and New Career Opportunities in the AI Era

* **The "LED Light" Paradox and Software Explosion**: As AI makes coding cheaper (similar to how LED lightbulbs cut lighting costs to 1/10), the global demand for software development will skyrocket rather than decrease. Today, even non-IT professionals (such as lawyers and doctors) are winning major Hackathons hosted by Anthropic.
* **New In-Demand Job Trends - Fixing "AI Garbage Code" & Platform Engineering**: Due to the ease of AI code generation, the market will face a massive influx of buggy MVPs and unstable projects. Consequently, long-term recruitment demand will surge for engineers specialized in fixing poorly written code, optimization, and Platform Engineering to automate Internal Developer Platforms (IDP) for enterprises.
* **Recruitment Reality in Vietnam**: Global tech giants continue to establish Technical Hubs in Vietnam to tap into local talent. Therefore, Vietnamese engineers must focus on building self-confidence, improving English proficiency, acquiring actual Domain Knowledge, and creating production-ready solutions rather than relying purely on minor demo exercises.

#### 2. Context Optimization Techniques and Controlling LLM Randomness

* **The Constant Context-Switching Error**: A common mistake among users is cramming too many unrelated topics into a single chat session (asking about travel, CV optimization, and software programming all at once). This constantly alters the Context Window, causing the AI to hallucinate quickly.
* **Temperature Mechanisms and Logit Scores**: Fundamentally, an LLM is a probabilistic engine that ranks logit scores for the next token. When setting `Temperature = 0`, the AI switches its calculation from Softmax to Argmax (always selecting the highest-scoring token) to produce deterministic and consistent answers.
* **The Difference Between Cloud APIs and Local Hosts**: Even with `Temperature = 0`, APIs from OpenAI or Amazon Bedrock can still yield slightly different results across separate runs. The core reason lies in GPU parallel computing causing floating-point rounding discrepancies, coupled with commercial Inference Optimization techniques (where providers batch short prompts from different users to reduce costs). To achieve 100% absolute consistency, engineers must host the model on local infrastructure.

#### 3. Amazon Q Business Ecosystem & Next-Gen Data Analytics Assistants

* **Building Extended Arms via MCP (Model Context Protocol)**: The concept of an AI Agent today goes beyond generating text—it must be capable of taking Action. By plugging in MCP hosts, AI Agents can interact directly with systems, schedule meetings, send automated emails, or connect seamlessly with Jira, Confluence, Microsoft Cloud, and Google Suite.
* **Automated Data Analysis Assistant**: Business users without any BI (Business Intelligence) background can simply upload raw Excel sheets to Amazon Q Business (or QuickSight Desktop), and the system will automatically analyze and visualize data into a comprehensive Dashboard within minutes.

#### 4. Case Study: UTMorpho Project Wins Hackathon in 36 Continuous Hours

* **Solving Real-World Pain Points**: Instead of chasing generic macro ideas, the team focused on saving time and tokens for front-end developers during UI adjustments. Typically, to modify a tiny detail on an AI-generated interface, developers have to request the AI to regenerate everything from scratch.
* **Multi-Agent Architecture of UTMorpho**: The project utilizes a Serverless model on AWS coordinating 3 specialized agents:
* *Agent 1 (Vision Agent)*: Reads images or sketches from the user's camera and parses them into a structured JSON file.
* *Agent 2 (Layout Agent)*: Receives the JSON file and calculates CSS structures, layouts, and dimensions.
* *Agent 3 (Design Agent)*: Takes the layout information and compiles it into clean, complete HTML/CSS code in real-time (Streaming UI).


* **Key Feature**: Integrates an intuitive visual Editor that allows developers to drag, drop, and rearrange components directly on the rendered interface and export a public HTML link for peer review.

#### 5. Enterprise-Grade Multi-Agent Architecture for Banking Business (VPBank Practice)

* **Business Problem - Credit Scoring for Startups**: Traditional loan approval systems require businesses to provide financial audits for 3 consecutive years and physical collateral. This prevents early-stage startups (which only possess intellectual property and have been operating for 3–6 months) from accessing capital. The solution is designing a Multi-Agent system to analyze multi-dimensional, non-traditional data points.
* **Specialized Multi-Agent System Design**:
* *Credit Committee Agent (Manager/Orchestrator)*: Acts as the council chair, distributing tasks and synthesizing the final report.
* *Financial Analyst Agent*: Performs deep-dive analysis on short-term financial reports and corporate cash flows.
* *Market Research Agent*: Analyzes market share (TAM, SAM, SOM), competitors, and market trends.
* *Team Evaluator Agent*: Gathers and evaluates the founders' capability based on tech portfolios, and social activity across Twitter (X), LinkedIn, and Facebook.
* *Risk Assessor Agent*: Holds the most critical role—monitoring the guardrails of other agents, filtering inputs/outputs to prevent data leakage, and mitigating Prompt Injection attacks to meet the strict compliance standards of the State Bank of Vietnam.



---

### Key Takeaways

#### Design Thinking

- **Business-Driven Mindset**: When designing any technological solution for large enterprises, one must always answer 4 core questions: Who uses it? What do they use it for? Why must they use it? When is the right time to deploy it?
- **Separation of Concerns (SoC)**: Each AI Agent should be assigned to a single specialized role supported by a clear backstory and System Prompt. This prevents Context Window overload and optimizes the model's attention allocation.

#### Technical Architecture

- Mastered **Determinism Control Mechanisms** in LLMs by configuring parameters like `Temperature`, `Top P`, and `Repeat Penalty` depending on the required output format (Creative text vs. structured JSON/Code).
- Gained a deep understanding of **AWS Backbone & CloudFront PoP (Points of Presence)** network infrastructures: How CDNs aggregate multi-tier requests to protect Origin Servers from volumetric DDoS or SYN Flood attacks using features like SYN Proxy.
- Realized the importance of managing infrastructure as code via **Terraform (IaC)** to track resource versions and maintain reproducibility across multiple AWS regions.

#### Modernization Strategy

- **ROI (Return on Investment) Measurement Strategy**: An AI project aiming for Enterprise executive approval must prove its worth through hard data (Numbers speak louder than words), such as calculating the payback period and annual corporate cost savings instead of just showcasing a technical demo.
- **Continuous Testing Strategy (Testing, Testing, Testing)**: For an AI system to be production-ready in strict environments, engineers must perform dynamic and deep downstream integration testing to guarantee the system handles edge cases when the AI generates incorrect formats.

---

### Practical Applications to Work

- **Mindful Configuration of Temperature**: Set `Temperature = 0` or `0.1` when generating structured formats like JSON/HTML for current projects to reduce syntax errors in brackets and commas.
- **Adopting Multi-Agent Architectures to Prevent Failures**: Instead of making a single chat interface handle an entire workflow, break down problems into independent sub-agents (following the UTMorpho model) and use a manager agent to cross-check results.
- **Enhancing Application Security**: Implement sensitive data filtering layers (Input/Output filtering) via AWS Lambda before passing data to LLMs to comply with organizational security regulations.
- **Transitioning to Infrastructure Management with Terraform**: Start writing Terraform code for AWS CloudFront and S3 services to eliminate manual configuration ("Click Engineering") on the AWS Console, enabling streamlined management and periodic rotation of API/Access Keys.
- **Focusing on Core Backend Knowledge**: Cultivate foundational software engineering skills, master data structures, and API contracts. AI is merely a tool that accelerates product development; the engineer's system design capabilities remain the ultimate deciding factor.

---

### Event Experience

Immersing myself in this **“FCAJ Community Day”** workshop was a mind-shifting experience. Moving away from textbook theories, the event brought forward raw, real-world corporate lessons. Highlights of the experience included:

#### Learning from High-Caliber Speakers

- Speakers from AWS Vietnam, VPBank, VIB, and Gothamic X shared invaluable lessons regarding the vast gap between building personal hobby projects at home versus deploying real products for millions of clients in the banking industry, where security and compliance are paramount.

#### Practical Technical Exposure

- My technical outlook expanded upon witnessing how AI agents collaborate under a Multi-Agent framework, automatically performing holistic market analysis ranging from financial indicators and social media data to the professional background of business founders.
- Understood the fierce reality behind the cost-optimization algorithms of major Cloud providers, and why AI still behaves probabilistically even when the temperature parameter is set to absolute zero.

#### Utilizing Modern Tools

- Witnessed data visualization achieved through simple Vietnamese natural language commands via the live demo of Amazon Q Business and QuickSight. The adoption of MCP (Model Context Protocol) opens a new frontier, allowing engineers to build genuine "extended arms" for artificial intelligence.

#### Networking and Engagement

- The organizers provided an exceptional networking environment across different seating tiers (including engaging those on the 36th floor via a Lucky Draw system). The event strongly fostered a spirit of proactivity, encouraging attendees to strike up conversations, seek collaborators, and inspire team synergy among young students.

#### Core Conclusions

- AI is driving down the cost of software development, which will spark a market explosion and present massive opportunities for those equipped with strong system design skills to tackle complex problems.
- Never abuse AI through blind copying and pasting (Ctrl+C & Ctrl+V) without understanding the underlying code architecture, as the repercussions in enterprise production environments are severe.
- When building any technology system, the most critical factor is not just that it runs, but that it operates **securely**, **reliably**, and genuinely **delivers user value**.

#### Event Imagery

![Event Participation Evidence Image](</images/4-EventParticipated/Event2/event2(0).jpg>)
![Event Participation Evidence Image](</images/4-EventParticipated/Event2/event2(1).jpg>)
> In summary, the event not only delivered deep technical insights into Prompt Engineering and AI-era software development models, but more importantly, it ignited a passion for disciplined self-learning and shaped the right professional mindset for the next generation of tech engineers.
