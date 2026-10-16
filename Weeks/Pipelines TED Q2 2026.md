TED 9-box:  
Values: exceeds expectations  
Performance: exceeds expectations

Continues:

* Izzi should continue to use her strong communication and documentation skills to successfully drive alignment on ambiguous projects. While working on the HealthSource coordinator and the retrieval workbench, she was responsible for ensuring that they would work with the rest of the retrieval domain, which required closely working with the Routing team and ensuring our two teams were in alignment. She also worked with the HS team to get our changes clearly communicated to them, prioritized in their roadmap, and tested. This level of communication is especially important in a remote working environment. Despite the challenges that came up throughout this process, Izzi continually pushed for clearer decision making and contracts between the teams. Ultimately, despite the challenges presented by working across verticals, Izzi’s resilience in getting the HS integration working resulted in successfully retrieving over 20% of the target charts for the project within the first two weeks of the project.  
* Izzi should continue to bring together her technical expertise with her product domain expertise in planning and building out projects. Izzi worked closely with the product, design, and operations teams to inform her system design choices and to account for a wide variety of edge cases. Ultimately, this allowed us to get to an MVP of the Retrieval Workbench in an extremely short timeline that was effective for most cases, with a clear plan for extensibility.  
* Izzi should continue extending her impact by helping others onboard. This was especially true during Matt Fusco’s rotation on the team, which was intentionally temporary. Due to Izzi’s collaboration with Matt, Matt was able to quickly ramp up to team processes. Izzi was able to delegate the right level of work in order for Matt to understand enough of the context to make significant contributions to the team.

Considers:

* Izzi should consider how she can more efficiently move through the entire end to end software development lifecycle. Occasionally, Izzi will get caught up in pieces of the process, such as the ideation and planning stage. At times she’d benefit from biasing more towards earlier prototyping, which would help to validate initial assumptions and inform next questions and steps. Similarly, in times of ambiguity when teams are struggling to reach alignment, Izzi could make a call and move forward with an implementation that incudes flexibility.   
* As Izzi grows into a more senior engineer, she should consider how she can contribute to discussions about product and system direction at an earlier stage in the development lifecycle. This includes advocating for tech debt work and ideas for future improvements of the product, particularly those outside of those proposed by product or ops users. This will allow her to shape the direction of the product, and drive technical decisions forward.

Goals  
R\&D transformation  
Scale the retrieval workbench to support \>1M record requests per month  
Add 3 roadmap items per quarter that support scalability

## TED 4/8/26

TED 9-box: 

* Values: meets expectations  
* Performance: meets expectations

Continues:

* Kit should continue to own projects end to end with a detail oriented approach, balancing this thoroughness with still delivering on tight timelines. Kit’s ownership includes discovery and planning, moving efficiently to implementation, thorough testing, and considering downstream effects of her changes. For example, during the implementation of Manual QA V2, she planned out the backend and integration with the frontend and built out a thorough test suite in a condensed timeline. Additionally, as part of her rebuild of the intake system, she quickly arrived at a plan to handle the complicated process of sending data through from the intake domain to  the platform domain to the retrieval domain, and documented and owned running the manual intake process for our pilot projects.   
* Kit should continue to drive forward discovery and decision making, particularly in the face of ambiguity. Even when given very minimal requirements, Kit is able to assess requirements, architectural implications, and potential edge cases and collaborate with cross-functional teams to surface risks early and put together technical plans. Given that so much of our work with Project Switchboard involves so much ambiguity, having this level of flexibility on getting to a solution, and being able to start on implementation even when not all decision have been made, means that Kit is still able to effectively deliver. 

Considers:

* Kit should consider how she can be more proactive about advocating for technical, product, and design direction for the team and zone. Some examples of this would be contributing more to group discussions about technical decisions, proactively thinking through scalability requirements, and in other ways contributing her opinions during roadmapping discussions.   
* Kit should consider how she can mentor other engineers on the team and help level up their technical and non-technical skills. Some specific ideas here are to talk through her thought process when doing system designs, how she goes about making decisions in ambiguous situations, and technical paradigms and tools that she learns. By helping to up level other members of the team, she can expand her impact beyond just her direct contributions.

**Goals**  
Operational excellence  
Decrease amount of engineering time required for support  
For 5 workflows that currently require engineering manual intervention: automate the manual process or introduce a runbook or script

## TED Information

TED 9-box: 

* Values: meets expectations  
* Performance: exceeds expectations

Continues:

* Charlie should continue doing extremely deep discovery and product planning that balances a number of different requirements for the projects that he works on. The main project that Charlie was working on for H2 2025 was the System of Record. This work required navigating a complex set of requirements, stakeholders, and long‑term scalability concerns, and Charlie delivered a solution that balanced immediate needs with future growth. This data model redesign work, and the associated architectural decision decisions, laid a crucial foundation for the system that will allow us to scale it to support the millions of requests that flow through the payer system, and extend it to support record retrievals beyond the payer business, ensuring that building on this baseline is a seamless process.  
* Charlie should continue being an excellent communicator. This shows up in a number of ways: he is able to explain technically complex ideas to non-technical audiences, work through technical problems with other software engineers and help them better understand and plan systems, lay out multiple options with clearly defined tradeoffs, and record decisions and edge cases to ensure continued alignment (since others can and do reference his diagrams and documents). By communicating his ideas in the above scenarios, Charlie is able to make sure his deep thinking benefits the entire zone and vertical.  
* Charlie should continue to invest time in improving our system’s resilience. He made a number of improvements including KEDA for FHIR to CCDA and Zip, database query performance, FIFO for Retrieval to Platform, and structured extraction reports from Snowflake. Together, these improvements have ensured that our data contracts are adhered to so that our data is correct, and that our system is able to handle larger volumes without breaking or requiring engineering intervention. Beyond the direct impacts, these changes have set a pattern for other similar components to use.

Considers:

* As we continue to build on top of our core data models, Charlie should consider how he can avoid becoming a bottleneck for system of record changes. Specifically, as it currently stands, Charlie is consulted for most changes across the zone, and his opinion is extremely valuable. However, as the system expands and the team grows, this won’t be sustainable, so Charlie (along with the zone leadership) should think through how to set guardrails in place to allow for continued high velocity on changes to the system.  
* Charlie should continue to consider the tradeoff between in depth planning and meeting the ambitious delivery timelines required by Project Switchboard. This is true both with the work that Charlie does directly and also with the work he advises others on. By determining when the potentially less optimal but faster decision is okay, it will help the whole team move faster when that’s okay, and then have the space to take the time on more complex decisions when that’s needed.

**Goals**  
Customer centric roadmap  
\> Expand switchboard to support use cases beyond payer  
\>\> Contribute to the work to run 1 non-payer use case  
R\&D transformation  
\> Scale the platform to support all risk adjustment volume  
\>\> Ensure all systems and databases have monitoring