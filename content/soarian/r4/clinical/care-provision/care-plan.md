---
title: CarePlan | R4 API
---

# CarePlan

* TOC
{:toc}

## Overview

The CarePlan resource describes the intention of how one or more practitioners plan to deliver care for a patient specific to an encounter.

Soarian Clinicals<sup>®</sup> supports a read-only Application Programming Interface (API). This API accepts `GET` and `POST` based [search](https://www.hl7.org/fhir/http.html#search) interactions. The response represents the most current information about the patient that is charted in Soarian Clinicals<sup>®</sup> at the time of the query. 

The search results include the following fields if they contain values:

* [CarePlan Id](http://hl7.org/fhir/r4/resource-definitions.html#Resource.id){:target="_blank"}
* [Status](http://hl7.org/fhir/r4/careplan-definitions.html#CarePlan.status){:target="_blank"}
* [Intent (plan)](http://hl7.org/fhir/r4/careplan-definitions.html#CarePlan.intent){:target="_blank"}
* [Category (assess-plan)](http://hl7.org/fhir/r4/careplan-definitions.html#CarePlan.category){:target="_blank"}
* [Subject (Patient Only)](http://hl7.org/fhir/r4/careplan-definitions.html#CarePlan.subject){:target="_blank"}
* [Encounter](http://hl7.org/fhir/r4/careplan-definitions.html#CarePlan.encounter){:target="_blank"}


## Terminology Bindings

<%= terminology_table(:soarian_care_plan, :r4) %>

## Search

Search for CarePlan resources that meet the specified query parameters:

	GET /CarePlan?:parameters

### Authorization Types

<%= authorization_types(provider: true, patient: true)%>

### Parameters

 Name         | Required?        | Type          | Description
--------------|------------------|---------------|--------------
 `_id`        | This, or `patient` | [`token`](http://hl7.org/fhir/R4/search.html#token)    | The logical resource ID associated with the resource.
 `patient`    | This, or `_id`     | [`reference`](http://hl7.org/fhir/r4/search.html#reference) | The patient who has the care plan. 
 `category`   | See notes        | [`token`](http://hl7.org/fhir/R4/search.html#token)    | The scope of the care plan. Example: `category=assess-plan`
 `encounter`  | No               | [`reference`](http://hl7.org/fhir/r4/search.html#reference) | The encounter associated with the care plan record. 
 `_count`     | No               | [`count`](https://hl7.org/fhir/r4/search.html#count)     | The maximum number of resources returned in a page.
 `_revincude` | No               | [`revinclude`](http://hl7.org/fhir/search.html#revinclude)| A request to include any Provenance resource in the bundle that refers to a CarePlan resource in the search results. Only supported with Provenance.

 Notes:

*	Either `_id` or `patient` and `category` is required.
*	The `category` parameter:
	*	May be combined with the `_id` parameter.
	*	Is required with the `patient` parameter.
	*	Only supports the code `assess-plan`.

### Headers

<%= headers fhir_json: true %>

### Example Search by Patient and Category

#### Request

	GET https://fhir-myrecord-sc.sandboxcerner.com/r4/0e885770-571b-4c0c-b30f-21df9a058d0d/CarePlan?patient=494454CC0E254A409CD98DA791EB2E16&category=assess-plan

#### Response

<%= headers status: 200 %>
<%= json(:SOARIAN_R4_CAREPLAN_SEARCH_BY_PT_CATEGORY) %>

Note: The examples provided here are non-normative and replaying them in the public sandbox is not guaranteed to yield the results shown on the site.

### Example Search by ID

#### Request

	GET https://fhir-myrecord-sc.sandboxcerner.com/r4/0e885770-571b-4c0c-b30f-21df9a058d0d/CarePlan?_id=494454CC0E254A409CD98DA791EB2E16.DDC.80014

#### Response

<%= headers status: 200 %>
<%= json(:SOARIAN_R4_CAREPLAN_SEARCH_BY_ID) %>

Note: The examples provided here are non-normative and replaying them in the public sandbox is not guaranteed to yield the results shown on the site.

### Errors

*	The common [errors](#errors) and [OperationOutcomes](https://www.hl7.org/fhir/r4/operationoutcome.html) may be returned.

## Retrieve by ID	

List an individual CarePlan resource by its ID:

	GET /CarePlan/:id

### Authorization Types

<%= authorization_types(provider: true, patient: true)%>


### Headers

<%= headers fhir_json: true %>

### Example

#### Request

	GET https://fhir-myrecord-sc.sandboxcerner.com/r4/0e885770-571b-4c0c-b30f-21df9a058d0d/CarePlan/494454CC0E254A409CD98DA791EB2E16.DDC.80014

#### Response

<%= headers status: 200 %>
<%= json(:SOARIAN_R4_CAREPLAN_READ_BY_ID) %>

Note: The examples provided here are non-normative and replaying them in the public sandbox is not guaranteed to yield the results shown on the site.






