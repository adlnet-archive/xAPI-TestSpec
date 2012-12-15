# Experience API
## Advanced Distributed Learning (ADL) Co-Laboratories

>This document was authored by members of the Experience API Working Group (see 
>list on pp. 7-8) in support of the Office of the Deputy Assistant Secretary of 
>Defense (Readiness) Advanced Distributed Learning (ADL) Initiative. Please 
>send all feedback and inquiries to helpdesk@adlnet.gov  

# Table of Contents
[1.0. Revision History](#1.0)  
[2.0. Role of the Experience API](#2.0)  
    [2.1. ADL's Role in the Experience API](#2.1)  
    [2.2. Contributors](#2.2)  
      [2.2.1. Working Group Participants](#2.2.1)  
      [2.2.2. Requirements Gathering Participants](#2.2.2)  
[3.0. Definitions](#3.0)  
    [Tin Can API (TCAPI)](#tcapi)  
[4.0. Statement](#4.0)  
    [4.1. Statement Properties](#4.1)  
      [4.1.1. ID](#4.1.1)  
      [4.1.2. Actor](#4.1.2)  
      [4.1.3. Verb](#4.1.3)  
      [4.1.4. Object](#4.1.4)  
      [4.1.5. Result](#4.1.5)  
      [4.1.6. Context](#4.1.6)  
      [4.1.7. Timestamp](#4.1.7)  
      [4.1.8. Stored](#4.1.8)  
      [4.1.9. Authority](#4.1.9)  
      [4.1.10. Voided](#4.1.10)  
    [4.2. Retrieval of Statements](#4.2)  
[5.0. Miscellaneous Types](#5.0)  
    [5.1. Document](#5.1)  
    [5.2. Language Map](#5.2)  
    [5.3. Extensions](#5.3)  
[6.0. Runtime Communication](#6.0)  
    [6.1. Encoding](#6.1)  
    [6.2. Version Header](#6.2)  
    [6.3. Concurrency](#6.3)  
    [6.4. Security](#6.4)  
      [6.4.1. Authentication Definitions](#6.4.1)  
      [6.4.2. OAuth Authorization Scope](#6.4.2)  
[7.0. Data Transfer (REST)](#7.0)  
    [7.1. Error Codes](#7.1)  
    [7.2. Statement API](#7.2)  
    [7.3. State API](#7.3)  
    [7.4. Activity Profile API](#7.4)  
    [7.5. Agent Profile API](#7.5)  
    [7.6. Cross Origin Requests](#7.6)  
    [7.7. Validation](#7.7)  
[Appendix A: Bookmarklet](#AppendixA)  
[Appendix B: Creating an "IE Mode" Request](#AppendixB)  
[Appendix C: Example definitions for activities of type "cmi.interaction"](#AppendixC)  

<a name="1.0"/>  
# 1.0 Revision History
__0.8 (Project Tin Can API Deliverable) to 0.9 (March 31, 2012):__
  
Rustici software, whom delivered Project Tin Can API, made modifications to the 
API prior to the April 2012 Kickoff Meeting. It was voted in this meeting to 
move those changes into the current spec and revision to 0.9.

__0.90 to 0.95 (August 31, 2012):__  

"Core" verbs and activity types were removed from the specification. References 
to these verbs in results, context, interactions, and activity definitions have 
also been removed. It is recommended that implementers prefer community defined 
verbs to creating their own verbs.
- Verbs, activity types, and extension keys are now URIs
- Restructured and added language around some of the other implementation details and scope.
- Changed from using a person-centric view of agents to a persona-centric view.
- Friend of a Friend (FOAF) agent merging requirement removed.
- Agent objects must now have exactly 1 uniquely identifying property, instead of at least one.

<a name="2.0"/> 
<a name="2.1"/> 
<a name="2.2"/> 
<a name="2.2.1"/> 
<a name="2.2.2"/> 
<a name="3.0"/> 
<a name="tcapi"/> 
<a name="4.0"/> 
<a name="4.1"/> 
<a name="4.1.1"/> 
<a name="4.1.2"/> 
<a name="4.1.3"/> 
<a name="4.1.4"/> 
<a name="4.1.5"/> 
<a name="4.1.6"/> 
<a name="4.1.7"/> 
<a name="4.1.8"/> 
<a name="4.1.9"/> 
<a name="4.1.10"/> 
<a name="4.2"/> 
<a name="5.0"/> 
<a name="5.1"/> 
<a name="5.2"/> 
<a name="5.3"/> 
<a name="6.0"/> 
<a name="6.1"/> 
<a name="6.2"/> 
<a name="6.3"/> 
<a name="6.4"/> 
<a name="6.4.1"/> 
<a name="6.4.2"/> 
<a name="7.0"/> 
<a name="7.1"/> 
<a name="7.2"/> 
<a name="7.3"/> 
<a name="7.4"/> 
<a name="7.5"/> 
<a name="7.6"/> 
<a name="7.7"/> 
<a name="AppendixA"/> 
<a name="AppendixB"/> 
<a name="AppendixC"/>   