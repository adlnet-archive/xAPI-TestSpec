# Experience API
## Advanced Distributed Learning (ADL) Co-Laboratories

>This document was authored by members of the Experience API Working Group (see 
>list on pp. 7-8) in support of the Office of the Deputy Assistant Secretary of 
>Defense (Readiness) Advanced Distributed Learning (ADL) Initiative. Please 
>send all feedback and inquiries to helpdesk@adlnet.gov  

# Table of Contents
[1.0. Revision History](#revhistory)  
[2.0. Role of the Experience API](#roleofxapi)  
    [2.1. ADL's Role in the Experience API](#adlrole)  
    [2.2. Contributors](#contributors)  
      [2.2.1. Working Group Participants](#wg)  
      [2.2.2. Requirements Gathering Participants](#reqparticipants)  
[3.0. Definitions](#defintions)  
    [Tin Can API (TCAPI)](#tcapi)  
[4.0. Statement](#statement)  
    [4.1. Statement Properties](#stmtprops)  
      [4.1.1. ID](#stmtid)  
      [4.1.2. Actor](#actor)  
      [4.1.3. Verb](#verb)  
      [4.1.4. Object](#object)  
      [4.1.5. Result](#result)  
      [4.1.6. Context](#context)  
      [4.1.7. Timestamp](#timestamp)  
      [4.1.8. Stored](#stored)  
      [4.1.9. Authority](#authority)  
      [4.1.10. Voided](#voided)  
    [4.2. Retrieval of Statements](#retstmts)  
[5.0. Miscellaneous Types](#misctypes)  
    [5.1. Document](#miscdocument)  
    [5.2. Language Map](#misclangmap)  
    [5.3. Extensions](#miscext)  
[6.0. Runtime Communication](#rtcom)  
    [6.1. Encoding](#encoding)  
    [6.2. Version Header](#versionheader)  
    [6.3. Concurrency](#concurrency)  
    [6.4. Security](#security)  
      [6.4.1. Authentication Definitions](#authdefs)  
      [6.4.2. OAuth Authorization Scope](#oauthscope)  
[7.0. Data Transfer (REST)](#datatransfer)  
    [7.1. Error Codes](#errorcodes)  
    [7.2. Statement API](#stmtapi)  
    [7.3. State API](#stateapi)  
    [7.4. Activity Profile API](#actprofapi)  
    [7.5. Agent Profile API](#agentprofapi)  
    [7.6. Cross Origin Requests](#cors)  
    [7.7. Validation](#validation)  
[Appendix A: Bookmarklet](#AppendixA)  
[Appendix B: Creating an "IE Mode" Request](#AppendixB)  
[Appendix C: Example definitions for activities of type "cmi.interaction"](#AppendixC)  

<a name="revhistory"/>  
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

<a name="roleofxapi"/>
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
 
<a name="adlrole"/>
## 2.1 ADL's Role in the Experience API  
ADL has taken a role of steward and facilitator in the development of the 
Experience API.  The Experience API is seen as one piece of the ADL Training 
and Learning Architecture, which facilitates learning anytime and anywhere. 
ADL views the Experience API as an evolved version of SCORM that can support 
similar use cases, but can also support many of the use cases gathered by ADL 
and submitted by those involved in distributed learning which SCORM could not 
enable.  
 
<a name="contributors"/> 
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

<a name="wg"/>
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
<a name="reqparticipants"/> 
## 2.2.2 Requirements Gathering Participants  
In collection of requirements for the Experience API, there were many people and 
organizations that provided invaluable feedback to SCORM, distributed learning 
efforts, and learning in general.  User Voice Site, Rustici Blog, etc.  

<a name="defintions"/> 
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

<a name="statement"/> 
#4.0 Statement  
The statement is the core of the XAPI.  All learning events are stored as statements 
such as: "I did this".  

<a name="stmtprops"/>
##4.1 Statement Properties:  
Actor, verb, and object are required, all other properties are optional. Properties 
can occur in any order, but are limited to one use each. Each property is discussed 
below.  

<table>
	<tr><th>Property</th><th>Type</th><th>Default</th><th>Description</th></tr>
	<tr><td>id</td><td>UUID</td><td></td>
	<td>UUID assigned by LRS or other trusted source.</td></tr>
	<tr><td><a href="#actor">actor</a></td><td>Object</td><td></td>
	<td>Who the statement is about, as an <a href="#agent">Agent</a> or 
		<a href="#group">Group</a> object. 'I'</td></tr>
	<tr><td><a href="#verb">verb</a></td><td>Object</td><td></td>
	<td>Action of the Learner or Team object. "Did".</td></tr>
	<tr><td><a href="#object">object</a></td><td>Object</td><td></td>
	<td>Activity, agent, or another statement that is the object of the statement, 
	"this". Note that objects which are provided as a value for this field should 
	include a "objectType" field. If not specified, the object is assumed to be 
	an activity.</td></tr>
	<tr><td><a href="#result">result</a></td><td>Object</td><td></td>
	<td>Result object, further details relevant to the specified verb.</td></tr>
	<tr><td><a href="#context">context</a></td><td>Object</td><td></td>
	<td>Context that gives the statement more meaning. Examples: Team actor is 
	working with, altitude in a flight simulator.</td></tr>
	<tr><td><a href="#timestamp">timestamp</a></td><td>Date/Time</td><td></td>
	<td>Timestamp (Formatted according to <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations">ISO 8601</a>) 
	of when what this statement describes happened. If not provided, LRS 
	should set this to the value of "stored" time.</td></tr>
	<tr><td><a href="#stored">stored</a></td><td>Date/Time</td><td></td>
	<td>Timestamp (Formatted according to <a href="https://en.wikipedia.org/wiki/ISO_8601#Durations">ISO 8601</a>) 
	of when this statement was recorded. Set by LRS.</td></tr>
	<tr><td><a href="#authority">authority</a></td><td>Object</td><td></td>
	<td>Agent who is asserting this statement is true. Verified by LRS based on 
	authentication, and set by LRS if left blank.</td></tr>
	<tr><td><a href="#voided">voided</a></td><td>Boolean</td><td>false</td>
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
<a name="stmtid"/> 
### 4.1.1 ID:  

The statement ID is a UUID which MAY be generated by the Learning Activity Provider. 
If a statement is posted without an ID, the LRS MUST assign one.  

<a name="actor"/>
### 4.1.2 Actor:  

The actor field contains an Agent or Group object, loosely inspired by Friend 
Of A Friend (FOAF, http://xmlns.com/foaf/spec/#term_Agent ), a widely accepted 
vocabulary for describing identifiable individuals and groups.  

<a name="agent"/>
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
<table>
	<tr><th>Property</th><th>Description</th></tr>
	<tr>
		<td>objectType</td>
		<td>"Agent" (Optional, except when used as a statement's object)</td>
	</tr>
	<tr><td>name</td><td>String (Optional)</td></tr>
	<tr>
		<td><a href="http://xmlns.com/foaf/spec/%22%20%5Cl%20%22term_mbox">mbox*</a></td>
		<td>String in the form "mailto:email address". (Note: Only emails that 
			have only ever been and will ever be assigned to this Agent, 
			but no others, should be used for this property and mbox_sha1sum).</td>
	</tr>
	<tr>
		<td><a href="http://xmlns.com/foaf/spec/%22%20%5Cl%20%22term_mbox_sha1sum">mbox_sha1sum*</a></td>
		<td>String containing the SHA1 hash of a mailto URI (such as goes in an mbox 
			property). An LRS MAY include Agents with a matching hash when a 
			request is based on an mbox.</td>
	</tr>
	<tr><td>openid*</td><td>The URI of an openid that uniquely identifies this agent.</td></tr>
	<tr><td>account*</td><td>An account object, <a href="#agentaccount">see below</a>.</td></tr>
</table>

<a name="agentaccount"/>
__Account__  

<table>
	<tr><th>Property</th><th>Description</th></tr>
	<tr>
		<td>homePage</td>
		<td>The URI to the canonical home page for the system the account is on. 
			This is based on FOAF's accountServiceHomePage.</td>
	</tr>
	<tr>
		<td>name</td>
		<td>The unique ID or name used to log in to this account. This is based 
			on FOAF's accountName.</td>
	</tr>
</table>  
An example using an opaque account:  
```
{
	"objectType": "Agent",
	"account": {
		"homePage": "http://www.example.com",
		"name": "1625378"
	}
}
```  
Agents are also important in relation to OAuth. See the section on 
[OAuth](#authdefs) for details.  

<a name="group"/>
#### 4.1.2.2 Group:
Groups are similar to Agents, represent collections of Agents, and can be used 
most places Agents can. Groups can either be anonymous or identified. Anonymous 
Groups MUST include a member property listing constituent Agents. Systems 
consuming Statements MUST consider all anonymous Groups distinct. Anonymous 
Groups are useful for describing collections of people where no ready identifier 
for the group is available, such as ad hoc teams.  

Identified Groups MUST, like Agents, include exactly one inverse functional 
identifier. Identified Groups MAY also include a member property listing 
constituent Agents. Inverse functional identifiers used for identified Groups 
SHOULD NOT be used for any Agents.  

Systems consuming Statements MUST NOT assume member Agents comprise an exact 
list of agents in an anonymous or identified Group.  

__Anonymous Group__  
<table>
	<tr><th>Property</th><th>Description</th></tr>
	<tr><td>objectType</td><td>"Group" (Required)</td></tr>
	<tr><td>name</td><td>String (Optional)</td></tr>
	<tr><td>member</td>
		<td>(array of) <a href="#agent">Agent</a> (not Group) objects representing 
			members of this Group.</td>
	</tr>
</table>

__Identified Group__  
<table>
	<tr><th>Property</th><th>Description</th></tr>
	<tr><td>objectType</td><td>"Group" (Required)</td></tr>
	<tr><td>name</td><td>String (Optional)</td></tr>
	<tr>
		<td><a href="http://xmlns.com/foaf/spec/%22%20%5Cl%20%22term_mbox">mbox*</a></td>
		<td>String in the form "mailto:email address". (Note: Only emails that 
			have only ever been and will ever be assigned to this Agent, 
			but no others, should be used for this property and mbox_sha1sum).</td>
	</tr>
	<tr>
		<td><a href="http://xmlns.com/foaf/spec/%22%20%5Cl%20%22term_mbox_sha1sum">mbox_sha1sum*</a></td>
		<td>String containing the SHA1 hash of a mailto URI (such as goes in an mbox 
			property). An LRS MAY include Agents with a matching hash when a 
			request is based on an mbox.</td>
	</tr>
	<tr><td>openid*</td><td>The URI of an openid that uniquely identifies this agent.</td></tr>
	<tr><td>account*</td><td>An account object, <a href="#agentaccount">see below</a>.</td></tr>
	<tr><td>member</td>
		<td>(array of) <a href="#agent">Agent</a> (not Group) objects representing 
			members of this Group.</td>
	</tr>
</table>  


<a name="verb"/>
### 4.1.3 Verb:

A verb defines what the action is between actors, activities, or most commonly, 
between an actor and activity. The Tin Can API does not specify any particular 
verbs, but rather defines how verbs are to be created. It is expected that verb 
lists exist for various communities of practice. Verbs appear in statements as 
objects consisting of a URI and a set of display names.

The Verb URI should identify the particular semantics of a word, not the word 
itself. For example, the English word "fired" could mean different things 
depending on context, such as "fired a weapon", "fired a kiln", or "fired an 
employee". In this case, a URI should identify one of these specific meanings, 
not the word "fired".

The Tin Can API does not specify any particular verbs (except the reserved 
“http://adlnet.gov/expapi/verbs/voided"), but rather defines how verbs are to 
be used. Communities of practice will develop verbs they find useful and make 
them available to the general community for use.

A verb in the Tin Can API is a URI, and denotes a specific meaning not tied to 
any particular language. For example, a particular verb URI such as 
http://example.org/firearms#fire or tag:example.com,2012:xQr73H might denote 
the action of firing a gun, or the verb URI http://example.com/فعل/خواندن 
might denote the action of reading a book. 

The person who comes up with a new verb should own the URI, or have permission 
from the owner to use the URI to denote a Tin Can API verb. The owner of a URI 
SHOULD make a human-readable description of the intended usage of the verb 
accessible at the URI.

__NOTE__: In some future version, this specification might specify additional 
machine-readable information about the verb be made available, but the choice 
to do so is postponed to monitor emerging practices and pain points. ADL plans 
to release a set of recommended verbs at the same time as this specification. 
Learning Activity Providers MAY use one these verbs, or other verb which have 
wide adoption, if applicable. The verb list to be created by ADL will include 
verbs corresponding to the verbs previously defined in this specification. If 
the meaning of one of those verbs is intended, Learning Activity Providers 
SHOULD use the corresponding ADL verb. Learning Activity Providers MAY create 
their own verbs instead, as needed.  

#### 4.1.3.1 Verb Object: 

The verb object is the representation of a verb that is actually included in 
a statement. In addition to referencing the verb itself via a URI, it includes 
a display property which provides the human-readable meaning of the verb in 
one or more languages.

The display property MUST NOT be used to alter the meaning of a statement, 
rather it MUST be used to illustrate the meaning which is already determined 
by the verb URI.

All statements SHOULD use the display property.  A system reading a statement 
MUST NOT use the display property to infer any meaning from the statement, 
rather it MUST use the verb URI to infer meaning, and the display property only 
for display to a human.  
<table>
	<tr><th>Property</th><th>Description</th><th>Example</th></tr>
	<tr>
		<td>id</td>
		<td>A URI that corresponds to a verb definition. Each verb definition 
			corresponds to the meaning of a verb, not the word. A URI should 
			be human-readable and contain the verb meaning.</td>
		<td>www.adlnet.gov/XAPIprofile/ran(travelled_a_distance)</td>
	</tr>
	<tr>
		<td>display</td>
		<td>A language map containing the human readable representation of the 
			verb in at least one language. This does not have any impact on the 
			meaning of the statement, but only serves to give a human-readable 
			display of the meaning already determined by the chosen verb.</td>
		<td>display : { "en-US" : "ran"}<br/>
			display : { "en-US" : "ran", "es" : "corrió" }</td>
	</tr>
</table>
<a name="object"/>
### 4.1.4 Object:  
The object of a statement is the Activity, Agent, or Statement that is the object 
of the statement, "this". Note that objects which are provided as a value for 
this field should include an "objectType" field. If not specified, the object 
is assumed to be an Activity.  

<a name="activity"/>
#### 4.1.4.1 – Activity as “object”
A statement may represent a Learning Activity as an object in the statement.  
<table>
	<tr><th>Property</th><th>Description</th></tr>
	<tr>
		<td>objectType</td>
		<td>Should always be "Activity" when present. Used in cases where type 
			cannot otherwise be determined, such as the value of a statement's 
			"object" field.</td>
	</tr>
	<tr><td><a href="#acturi">id</a></td><td>URI. If a URL, the URL should refer to metadata for this activity.</td></tr>
	<tr><td><a href="#actdef">definition</a></td><td>Metadata, See below</td></tr>
</table>
<a name="acturi"/>
__Activity URI__  
An activity URI must always refer to a single unique activity. There may be 
corrections to that activity's definition. Spelling fixes would be appropriate, 
for example, but changing correct responses would not.  

The activity URI is unique, and any reference to it always refers to the same 
activity. Activity Providers must ensure this is true and the LRS may not attempt 
to treat multiple references to the same URI as references to different activities, 
regardless of any information which indicates two authors or organizations may 
have used the same activity URI.    

When defining an activity URI, care must be taken to make sure it will not be 
re-used. It should use a domain the creator controls or has been authorized to 
use for this purpose, according to a scheme the domain owner has adopted to make 
sure activity URIs within that domain remain unique.  

Any state or statements stored against an activity URI must be compatible and 
consistent with any other state or statements that are stored against the same 
activity URI, even if those statements were stored in the context of a new 
revision or platform.   

NOTE: The prohibition against an LRS treating references to the same activity 
URI as two different activities, even if the LRS can positively determine that 
was the intent, is crucial to prevent activity id creators from creating ids 
that could be easily duplicated, as intent would be indeterminable should a 
conflict with another system arise.  

<a name="actdef"/>
__Activity Definition__  
<table>
	<tr><th>Property</th><th>Description</th></tr>
	<tr><td>name</td><td><a href="#misclangmap">Language Map</a>, The human readable/visual name of the activity</td></tr>
	<tr><td>description</td><td><a href="misclangmap">Language Map</a>, A description of the activity</td></tr>
	<tr>
		<td>type</td>
		<td>URI, the type of activity. Note, URI fragments (sometimes called 
			relative URLs) are not valid URIs. Similar to verbs, we recommend 
			that Learning Activity Providers look for and use established, 
			widely adopted, activity types.</td>
	</tr>
	<tr>
		<td>interactionType | correctResponsesPattern | choices | scale | 
			source | target | steps</td>
		<td><a href="#interactionacts">See "Interaction Activities"</a></td>
	</tr>
	<tr><td>extensions</td><td>A map of other properties as needed (see: <a href="#miscext">Extensions</a>)</td></tr>
</table>  
An LRS should update its internal representation of an activity's definition 
upon receiving a statement with a different definition of the activity from the 
one stored, but only if it considers the Learning Activity Provider to have the 
authority to do so.  

Activities may be defined in XML according to the schema http://www.adlnet.gov/xapi. 
LRS's MAY attempt to look up an XML document at the URL given by the activity URI, 
and check if it conforms to the Experience API schema. If it does, the LRS SHOULD 
fill in its internal representation of the activities definition based on that 
document. Note that activity URI's are not required to resolve to such metadata.  

Note that multiple activities may be defined in the same metadata document. The 
LRS MAY choose whether to store information about activities other than those 
it has received statements for or not.  

As part of each group of activities, the activity metadata document may define 
information about an associated activity provider, which the LRS SHOULD consider 
the authoritative source for statements about the activity.  

<a name="interactionacts"/>
__Interaction Activities__  

Traditional e-learning has included structures for interactions or assessments. 
As a way to allow these practices and structures to extend Experience API's 
utility, this specification include built in definitions for interactions which 
borrows from the CMI data model. These definitions are intended to provide a 
simple and familiar utility for recording interaction data. These definitions 
are simple to use, and consequently limited. It is expected that communities of 
practice requiring richer interactions definitions will do so through the use 
of extensions to an activity's type and definition.  

When defining interaction activities, the activity type: 
"http://www.adlnet.gov/experienceapi/activity-types/cmi.interaction" SHOULD 
be used, and a valid interactionType MUST be specified. If interactionType 
is specified, an LRS processing MAY validate the remaining properties as 
specified in the table below, and return HTTP 400 "Bad Request" if the 
remaining properties are not valid for the interaction type.  
<table>
	<tr><th>Property</th><th>Description</th></tr>
	<tr>
		<td>interactionType</td>
		<td>As in "cmi.interactions.n.type" as defined in the SCORM 2004 4th 
			edition Runtime Environment.</td>
	</tr>
	<tr>
		<td>correctResponsesPattern</td>
		<td>An array of strings, corresponding to 
			"cmi.interactions.n.correct_responses.n.pattern" as defined in 
			the SCORM 2004 4th edition Runtime Environment, where the final 
			<em>n</em> is the index of the array.</td>
	</tr>
	<tr>
		<td>choices | scale | source | target | steps</td>
		<td>Array of interaction components specific to the given interaction type (see below).</td>
	</tr>
</table>  

__Interaction Components__  

Interaction components are defined as follows:  
<table>
	<tr><th>Property</th><th>Description</th></tr>
	<tr>
		<td>id</td>
		<td>As in "cmi.interactions.n.id" as defined in the SCORM 2004 4th 
			edition Runtime Environment</td> 
	<tr>
		<td>description</td> 
		<td><a href="misclangmap">Language Map</a>, a description of the interaction component 
			(for example, the text for a given choice in a multiple-choice interaction)</td>
	</tr>
</table>  

The following table shows the supported lists of CMI interaction components for 
an interaction activity with the given interactionType.  
<table>
	<tr><th>interactionType</th><th>supported component list(s)</th><tr>
	<tr><td>choice, sequencing</td><td>choices</td></tr>
	<tr><td>likert</td><td>scale</td></tr>
	<tr><td>matching</td><td>source, target</td></tr>
	<tr><td>performance</td><td>steps</td></tr>
	<tr><td>true-false, fill-in, numeric, other</td><td>[No component lists defined]</td></tr>
</table>

>See [Appendix C](#AppendixC) for examples of activity definitions for each of the cmi.interaction types.

<a name="agentasobj"/>
<a name="stmtasobj"/> 
<a name="result"/>
<a name="score"/> 
<a name="context"/> 
<a name="timestamp"/> 
<a name="stored"/> 
<a name="authority"/> 
<a name="voided"/> 
<a name="retstmts"/> 
<a name="misctypes"/> 
<a name="miscdocument"/> 
<a name="misclangmap"/> 
<a name="miscext"/> 
<a name="rtcom"/> 
<a name="encoding"/> 
<a name="versionheader"/> 
<a name="concurrency"/> 
<a name="security"/> 
<a name="authdefs"/> 
<a name="oauthscope"/> 
<a name="datatransfer"/> 
<a name="errorcodes"/> 
<a name="stmtapi"/> 
<a name="stateapi"/> 
<a name="actprofapi"/> 
<a name="agentprofapi"/> 
<a name="cors"/> 
<a name="validation"/> 
<a name="AppendixA"/> 
<a name="AppendixB"/> 
<a name="AppendixC"/>   
