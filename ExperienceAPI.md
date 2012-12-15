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
- Restructured and added language around some of the other implementation 
details and scope.
- Changed from using a person-centric view of agents to a persona-centric 
view.
- Friend of a Friend (FOAF) agent merging requirement removed.
- Agent objects must now have exactly 1 uniquely identifying property, instead 
of at least one.

<a name="2.0"/>
# 2.0 Role of the Experience API  
The Experience API is a service that allows for statements of experience 
(typically learning experiences, but could be any experience) to be delivered 
to and stored securely in a Learning Record Store. The Experience API is 
dependent on Learning Activity Providers to create and track learning experiences; 
this specification provides a data model and associated components on how to 
accomplish these tasks.  
Specifically, the Experience API provides:  
- Structure and definition of statement, state, learner, activity and objects, 
which are the means by which experiences are conveyed by a Learning Activity Provider.
- Data Transfer methods for the storage and retrieval (but not validation) of 
these objects to/from a Learning Record Store.  Note that the systems storing 
or retrieving records need not be Learning Activity Providers. LRSs may 
communicate with other LRSs, or reporting systems.
- Security methods allowing for the trusted exchange of information between 
the Learning Record Store and trusted sources.  

The Experience API is the first of many potential specifications that will merge 
to create a higher architecture of online learning and training. Authentication 
services, querying services, visualization services, and personal data services 
are some examples of additional components that the Experience API is designing 
to work alongside. While the implementation details of these services are not 
specified here, the Experience API is designed with these components in mind.  
 
<a name="2.1"/>
## 2.1 ADL's Role in the Experience API  
ADL has taken a role of steward and facilitator in the development of the 
Experience API.  The Experience API is seen as one piece of the ADL Training 
and Learning Architecture, which facilitates learning anytime and anywhere. 
ADL views the Experience API as an evolved version of SCORM that can support 
similar use cases, but can also support many of the use cases gathered by ADL 
and submitted by those involved in distributed learning which SCORM could not 
enable.  
 
<a name="2.2"/> 
##2.2 Contributors
My thanks to everyone who contributed to the Experience API project. Many of 
you have called into the weekly meetings and helped to shape the specification 
into something that is useful for the entire distributed learning community. 
Many of you assisted in releasing code samples, products, and documentation to 
aid those who are creating and adopting the specification.  I'd also like to 
thank all of those who were involved in supplying useful, honest information 
about your organization's use of SCORM and other learning best practices. 
Through the use-cases, shared experiences, and knowledge you have shared, ADL 
and the community clearly identified the first step in creating the Training 
and Learning Architecture--the Experience API.  You are truly the community 
leaders on which we depend to make our training and education the very best.  

Kristy S. Murray, Ed.D.  
Director, ADL Initiative  
OSD, Training Readiness & Strategy (TRS)  

<a name="2.2.1"/>
## 2.2.1 Working Group Participants  
<table>
	<tr><th>Name:</th><th>Organization:</th></tr>
	<tr><td>Aaron Silvers</td><td>ADL</td></tr>
	<tr><td>Jonathan Poltrack</td><td>ADL</td></tr>
	<tr><td>Al Bejcek</td><td>NetDimensions</td></tr>
	<tr><td>Ali Shahrazad</td><td>SaLTBOX</td></tr>
	<tr><td>Andrew Downes</td><td> </td></tr>
	<tr><td>Andy Johnson</td><td>ADL</td></tr>
    <tr><td>Andy Whitaker</td><td>Rustici Software</td></tr>
	<tr><td>Anthony Altieri</td><td>American Red Cross</td></tr>
	<tr><td>Anto Valan</td><td>Omnivera Learning Solutions</td></tr>
	<tr><td>Avron Barr</td><td>Aldo Ventures, Inc.</td></tr>
	<tr><td>Ben Clark</td><td>Rustici Software</td></tr>
	<tr><td>Bill McDonald</td><td>Boeing</td></tr>
	<tr><td>Brian J. Miller</td><td>Rustici Software</td></tr>
	<tr><td>Chad Udell</td><td>Float Mobile Learning</td></tr>
	<tr><td>Dan Allen</td><td>Litmos</td></tr>
	<tr><td>Dan Kuemmel</td><td>Sentry Insurance</td></tr>
	<tr><td>Dave Mozealous</td><td>Articulate</td></tr>
	<tr><td>David Ells</td><td>Rustici Software</td></tr>
	<tr><td>Eric Johnson</td><td>Planning and Learning Technologies, Inc.</td></tr>
	<tr><td>Fiona Leteney</td><td>Feenix e-learning</td></tr>
	<tr><td>Greg Tatka</td><td>Menco Social Learning</td></tr>
	<tr><td>Ingo Dahn</td><td>University Koblenz-Landau</td></tr>
	<tr><td>Jason Haag</td><td>ADL</td></tr>
	<tr><td>Jeff Place</td><td>Questionmark</td></tr>
	<tr><td>Jennifer Cameron</td><td>Sencia Corporate Web Solutions</td></tr>
	<tr><td>Jeremy Brockman</td><td> </td></tr>
	<tr><td>Joe Gorup</td><td>CourseAvenue</td></tr>
	<tr><td>John Kleeman</td><td>Questionmark</td></tr>
	<tr><td>Kris Miller</td><td>edcetra Training</td></tr>
	<tr><td>Kris Rockwell</td><td>Hybrid Learning Systems</td></tr>
	<tr><td>Lang Holloman</td><td> </td></tr>
	<tr><td>Lou Wolford</td><td>ADL</td></tr>
	<tr><td>Luke Hickey</td><td>dominKnow</td></tr>
	<tr><td>Marcus Birtwhistle</td><td>ADL</td></tr>
	<tr><td>Mark Davis</td><td>Exambuilder</td></tr>
	<tr><td>Megan Bowe</td><td>Rustici Software</td></tr>
	<tr><td>Melanie VanHorn</td><td>ADL</td></tr>
	<tr><td>Michael Flores</td><td>Here Everything's Better</td></tr>
	<tr><td>Mike Palmer</td><td>OnPoint Digital</td></tr>
	<tr><td>Mike Rustici</td><td>Rustici Software</td></tr>
	<tr><td>Nik Hruska</td><td>ADL</td></tr>
	<tr><td>Patrick Kedziora</td><td>Kedzoh</td></tr>
	<tr><td>Paul Roberts</td><td>Questionmark</td></tr>
	<tr><td>Rich Chetwynd</td><td>Litmos</td></tr>
	<tr><td>Richard Fouchaux</td><td>Ontario Human Rights  Commission</td></tr>
	<tr><td>Richard Lenz</td><td>Organizational Strategies, Inc.</td></tr>
	<tr><td>Rick Raymer</td><td>Serco</td></tr>
	<tr><td>Rob Chadwick</td><td>ADL</td></tr>
	<tr><td>Robert Lowe</td><td></td></tr>
	<tr><td>Russell Duhon</td><td>SaLTBOX</td></tr>
	<tr><td>Stephen Trevorrow</td><td>Problem Solutions, LLC.</td></tr>
	<tr><td>Steve Baumgartner</td><td></td></tr>
	<tr><td>Steve Flowers</td><td>XPConcept</td></tr>
	<tr><td>Thomas Ho</td><td></td></tr>
	<tr><td>Tim Martin</td><td>Rustici Software</td></tr>
	<tr><td>Tom Creighton</td><td>ADL</td></tr>
	<tr><td>Walt Grata</td><td>ADL</td></tr>
</table> 
<a name="2.2.2"/> 
## 2.2.2 Requirements Gathering Participants  
In collection of requirements for the Experience API, there were many people and 
organizations that provided invaluable feedback to SCORM, distributed learning 
efforts, and learning in general.  User Voice Site, Rustici Blog, etc.  

<a name="3.0"/> 
# 3.0 Definitions  

__Experience API (XAPI)__: The API defined in this document, the product of 
"Project Tin Can API". A simple, lightweight way for any permitted actor to store 
and retrieve extensible learning records, learner and learning experience profiles, 
regardless of the platform used.  

<a name="tcapi"/>
__Tin Can API (TCAPI)__: The previous name of the API defined in this document.  

__Learning Activity Provider (AP)__: The software object that is communicating with 
the LRS to record information about a learning experience. May be similar to a SCORM 
package as it is possible to bundle assets with the software object that does this 
communication, but may also be separate from the experience it is reporting about.

__Learning Activity (activity)__: Like a SCORM Activity, a unit of instruction, 
experience, or performance that is to be tracked.

__Statement__: A simple statement consisting of <Actor (learner)> <verb> <object>, 
with <result>, in <context> to track an aspect of a learning experience. A set of 
several statements may be used to track complete details about a learning experience.

__Learning Record Store (LRS)__: A system that stores learning information. Currently, 
most LRSs are Learning Management Systems (LMSs), however this document uses the term 
LRS to be clear that a full LMS is not necessary to implement the XAPI. The XAPI 
is dependent on an LRS to function correctly.

__Learning Management System (LMS)__: Provides the tracking functionality of an LRS, 
but provides additional administrative and reporting functionality. In this document 
the term will be used when talking about existing systems that implement learning 
standards. The XAPI can work independently of an LMS, but is built with knowledge 
of the suite of services an LMS provides.

__Service__: A software component responsible for one or more aspects of the distributed 
learning process. An LMS typically combines many services to design a complete learning 
experience.

__Registration__: If the LRS is an LMS, it likely has a concept of registration, 
an instance of a learner signing up for a particular learning activity. The LMS may 
also close the registration at some point when it considers the learning experience 
complete. For Experience API purposes, a registration may be applied more broadly; an 
LMS could assign a group of students to a group of activities and track all related 
statements in one registration. Note: activity providers are cautioned against reporting 
registration other than when assigned by an LRS. An LRS that assigns registrations is 
likely to reject statements containing unassigned registration IDs.

__State__: Similar to SCORM suspend data, but allows storage of arbitrary key/document 
pairs. The LRS does not have to retain state once the learning experience is considered 
"done" (LRS has closed its "registration").

__Profile__: A construct where information about the learner or activity is kept, 
typically in name/document pairs that have meaning to an instructional system component.

__Authentication__: The concept of verifying the identity of a user or system. This 
allows interactions between the two “trusted” parties.

__Authorization__: The affordance of permissions based on a user or system's role: 
the process of making one user or system "trusted" by another.

__Community of Practice__: A group, usually connected by a common cause, role or 
purpose, which operates in a common modality.

<a name="4.0"/> 
#4.0 Statement  
The statement is the core of the XAPI.  All learning events are stored as statements 
such as: "I did this".  

<a name="4.1"/>
##4.1 Statement Properties:  
Actor, verb, and object are required, all other properties are optional. Properties 
can occur in any order, but are limited to one use each. Each property is discussed 
below.  

<table>
	<tr><th>Property</th><th>Type</th><th>Default</th><th>Description</th></tr>
	<tr><td>id</td><td>UUID</td><td></td>
	<td>UUID assigned by LRS or other trusted source.</td></tr>
	<tr><td>actor</td><td>Object</td><td></td>
	<td>Who the statement is about, as an Agent or Group object. 'I'</td></tr>
	<tr><td>verb</td><td>Object</td><td></td>
	<td>Action of the Learner or Team object. "Did".</td></tr>
	<tr><td>object</td><td>Object</td><td></td>
	<td>Activity, agent, or another statement that is the object of the statement, 
	"this". Note that objects which are provided as a value for this field should 
	include a "objectType" field. If not specified, the object is assumed to be 
	an activity.</td></tr>
	<tr><td>result</td><td>Object</td><td></td>
	<td>Result object, further details relevant to the specified verb.</td></tr>
	<tr><td>context</td><td>Object</td><td></td>
	<td>Context that gives the statement more meaning. Examples: Team actor is 
	working with, altitude in a flight simulator.</td></tr>
	<tr><td>timestamp</td><td>Date/Time</td><td></td>
	<td>Timestamp (Formatted according to <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations">ISO 8601</a>) 
	of when what this statement describes happened. If not provided, LRS 
	should set this to the value of "stored" time.</td></tr>
	<tr><td>stored</td><td>Date/Time</td><td></td>
	<td>Timestamp (Formatted according to <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations">ISO 8601</a>) 
	of when this statement was recorded. Set by LRS.</td></tr>
	<tr><td>authority</td><td>Object</td><td></td>
	<td>Agent who is asserting this statement is true. Verified by LRS based on 
	authentication, and set by LRS if left blank.</td></tr>
	<tr><td>voided</td><td>Boolean</td><td>false</td>
	<td>Indicates that the statement has been voided (see below)</td></tr>
</table>  
Aside from (potential or required) assignments of properties during initial 
processing ("id", "authority", "stored", "timestamp"), and the special case of 
updating the "voided" flag, statements are immutable. Note that the content of 
activities that are referenced in statements are not considered part of the 
statement itself. So while the statement is immutable, the activities referenced 
by that statement are not. This means a deep serialization of a statement into 
JSON will change if the referenced activities change.  

Example of a simple statement:  
```
{
	"id":"fd41c918-b88b-4b20-a0a5-a4c32391aaa0",
	"actor":{
		"objectType": "Agent",
		"name":"Project Tin Can API",
		"mbox":"mailto:user@example.com"
	},
	"verb":{
		"id":"http://adlnet.gov/expapi/verbs/created",
		"display":{ "en-US":"created" }
	},
	"object":{
		"id":"http://example.adlnet.gov/xapi/example/simplestatement",
		"definition":{
		"name":{ "en-US":"simple statement" },
		"description":{ "en-US":"A simple Experience API statement. Note that the LRS 
		does not need to have any prior information about the actor (learner), the 
		verb, or the activity/object." }
		}
	}
}
```   
Simplest possible statement using all properties that MUST or SHOULD be used:  
```
{
	"actor":{
		"objectType": "Agent",
		"mbox":"mailto:xapi@adlnet.gov"
	},
	"verb":{
		"id":"http://adlnet.gov/expapi/verbs/created",
		"display":{
			"en-US":"created"
		}
	},
	"object":{
		"id":"http://example.adlnet.gov/xapi/example/activity"
	}
}
```   
Typical simple completion with verb "attempted":  
```
{
	"actor":{
        "objectType": "Agent",
		"name":"Example Learner",
		"mbox":"mailto:example.learner@adlnet.gov"
	},
	"verb":{
		"id":"http://adlnet.gov/expapi/verbs/attempted",
		"display":{
			"en-US":"attempted"
		}
	},
	"object":{
		"id":"http://example.adlnet.gov/xapi/example/simpleCBT",
		"definition":{
			"name":{
				"en-US":"simple CBT course"
			},
			"description":{
				"en-US":"A fictitious example CBT course."
			}
		}
	},
	"result":{
		"score":{
			"scaled":0.95
		},
		"success":true,
		"completion":true
	}
}
```  
<a name="4.1.1"/> 
### 4.1.1 ID:  

The statement ID is a UUID which MAY be generated by the Learning Activity Provider. 
If a statement is posted without an ID, the LRS MUST assign one.  

<a name="4.1.2"/>
### 4.1.2 Actor:  

The actor field contains an Agent or Group object, loosely inspired by Friend 
Of A Friend (FOAF, http://xmlns.com/foaf/spec/#term_Agent ), a widely accepted 
vocabulary for describing identifiable individuals and groups.  

#### 4.1.2.1 Agent:  

An Agent object is identified by an email address (or its hash), OpenID, or 
account on some system (such as twitter), but only for values where any two 
Agents that share the same identifying property definitely represent the same 
identity. The term used for properties with that characteristic is "inverse 
functional identifiers”.  In addition to the standard inverse functional 
properties from FOAF of mbox, mbox_sha1sum, and openid, account is an inverse 
functional property in XAPI Agents.  

For reasons of practicality and privacy, TCAPI Agents MUST be identified by 
one and only one inverse functional identifier. Agents MUST NOT include more 
than one inverse functional identifier. If an Activity Provider is concerned 
about revealing identifying information such as emails, it SHOULD instead use 
an account with an opaque account name to identify the person.  

The table below lists all properties of Agent objects. Inverse functional 
identifiers are marked with a *."
 
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
