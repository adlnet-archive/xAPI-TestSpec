# Experience API
## Advanced Distributed Learning (ADL) Co-Laboratories

>This document was authored by members of the Experience API Working Group (see 
>list on pp. 7-8) in support of the Office of the Deputy Assistant Secretary of 
>Defense (Readiness) Advanced Distributed Learning (ADL) Initiative. Please 
>send all feedback and inquiries to helpdesk@adlnet.gov  

# Table of Contents
[1.0. Revision History](#1.0)  
2.0. Role of the Experience API  
  2.1. ADL's Role in the Experience API  
  2.2. Contributors  
    2.2.1. Working Group Participants  
    2.2.2. Requirements Gathering Participants  
3.0. Definitions  
  Tin Can API (TCAPI)  
4.0. Statement  
  4.1. Statement Properties  
    4.1.1. ID  
    4.1.2. Actor  
    4.1.3. Verb  
    4.1.4. Object  
    4.1.5. Result  
    4.1.6. Context  
    4.1.7. Timestamp  
    4.1.8. Stored  
    4.1.9. Authority  
    4.1.10. Voided  
  4.2. Retrieval of Statements  
5.0. Miscellaneous Types  
  5.1. Document  
  5.2. Language Map  
  5.3. Extensions  
6.0. Runtime Communication  
  6.1. Encoding  
  6.2. Version Header  
  6.3. Concurrency  
  6.4. Security  
    6.4.1. Authentication Definitions  
    6.4.2. OAuth Authorization Scope  
7.0. Data Transfer (REST)  
  7.1. Error Codes  
  7.2. Statement API  
  7.3. State API  
  7.4. Activity Profile API  
  7.5. Agent Profile API  
  7.6. Cross Origin Requests  
  7.7. Validation  
Appendix A: Bookmarklet  
Appendix B: Creating an "IE Mode" Request  
Appendix C: Example definitions for activities of type "cmi.interaction"  

<a name="1.0"/>  
# 1.0 Revision History
_0.8 (Project Tin Can API Deliverable) to 0.9 (March 31, 2012):_
  
Rustici software, whom delivered Project Tin Can API, made modifications to the 
API prior to the April 2012 Kickoff Meeting. It was voted in this meeting to 
move those changes into the current spec and revision to 0.9.

_0.90 to 0.95 (August 31, 2012):_  

"Core" verbs and activity types were removed from the specification. References 
to these verbs in results, context, interactions, and activity definitions have 
also been removed. It is recommended that implementers prefer community defined 
verbs to creating their own verbs.
- Verbs, activity types, and extension keys are now URIs
- Restructured and added language around some of the other implementation details and scope.
- Changed from using a person-centric view of agents to a persona-centric view.
- Friend of a Friend (FOAF) agent merging requirement removed.
- Agent objects must now have exactly 1 uniquely identifying property, instead of at least one.

