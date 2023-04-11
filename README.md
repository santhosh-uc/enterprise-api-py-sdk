# UniCourt Python SDK
The UniCourt SDK provides simplified access to the UniCourt API for applications written in the Python programming language.


## Documentation

See the API documentation here : [UniCourt API docs](https://docs.unicourt.com/direct-links/download-api-specification).

See the UniCourt data model here (requires UniCourt account): [UniCourt Data Model](https://docs.unicourt.com/enterpriseapi/unicourt_data_model_ui).

### Requirements

-   Python >=3.6

## Installation
You can use the source code if you want to modify the package and use it as per your need. If you just want to use the package, just run:
```sh
pip install --upgrade unicourt
```

Install from source :

```sh
python setup.py install
```

## Pre-request and Configuration
You need a UniCourt account with API access :  [Subscription Plans](https://unicourt.com/pricing)

You will find clientId and secret here: [Client Secrets](https://app.unicourt.com/developers/enterpiseAPI)

## Getting Started
The Python script you see here takes two command line arguments i.e clientId and secret, to execute the script copy and paste the code to a file (sample.py) and run the script in a terminal as shown in the example below.

Example : 
- python sample.py [your client id] [your secret]
- python sample.py G3cfixgetVzfaoszGOBp5LPGtih1nMJ9 u6PTti57IjPlrwU5MzOwLBD2MCwx-IEbo8sTStTivh1I-EqQ8Jcm27Gfo2GhpHCw

```python
import unicourt
from unicourt import *

# Get CLIENT_ID and CLIENT_SECRET from your account
unicourt.CLIENT_ID = "G3cfixgetVzfaoszGOBp5LPGtih1nMJ9"
unicourt.CLIENT_SECRET = "u6PTti57IjPlrwU5MzOwLBD2MCwx-IEbo8sTStTivh1I-EqQ8Jcm27Gfo2GhpHCw"

# Authenticate to generate a access token, below line will return
# a tuple consisting of authentication object and http status code.
# You can generate up to 10 authentication tokens so be sure to use
# invalidate_token() method to invalidate the token once you are done
# or store the token securely and use it for subsequent requests.
auth_obj, http_status_code = Authentication.generate_new_token()

# Get Area Of Law details.
court_standards_obj, http_status_code = CourtStandards.get_areas_of_law(
    q='name:"Personal Injury"',
    page_number=1,
    sort="name",
    order="asc")
for court_standard_obj in court_standards_obj.area_of_law_array:
    print("Area Of Law Id : ", court_standard_obj.area_of_law_id)


# Get Judge details.
judge_obj, http_status_code = JudgeAnalytics.search_normalized_judges(
    q="name:(ANN H. PARK)")
for judge in judge_obj.norm_judge_search_result_array:
    print("Norm Judge Id :", judge.norm_judge_id)

# Get Attorney details.
attorney_obj, http_status_code = AttorneyAnalytics.search_normalized_attorneys(
    q="name:(PURDY STUART JAMES)",
    page_number=1
)
for attorney in attorney_obj.norm_attorney_search_result_array:
    print("Attorney Name :", attorney.name)
    print("Norm Attorney Id :", attorney.norm_attorney_id)

# Invalidate the generated access token
Authentication.invalidate_token()


```
## Python SDK Usage
UniCourt API documentation for Python sdk 

| Class | Method | Description |
| --- | --- | --- |
| Authentication | generate_new_token | This endpoint allows you to generate a new access token, which is a required field for all UniCourt API endpoints except for the Authentication API. To generate a new token, you must provide your Client ID and Client Secret ID which you can find by logging into your UniCourt account. At any time, you can have a maximum of 10 active access tokens. The tokens never expire and, if you make a request which would otherwise lead to you having more than 10 active tokens, you will receive an error message. | 
| Authentication | list_all_token_ids | An endpoint which allows you to view all active access tokens associated with your Client ID and Client Secret ID. | 
| Authentication | invalidate_token | An endpoint which allows you to invalidate a given access token. | 
| Authentication | invalidate_all_tokens | An endpoint which allows you to invalidate all existing access tokens associated with your UniCourt account. | 
| Usage | get_billing_cycles | An endpoint to obtain information on the previous 12 billing cycles. | 
| Usage | get_billing_usage_by_billing_cycle | An endpoint to obtain information on API usage for a specific billing cycle. | 
| Usage | get_daily_usage_by_date | An endpoint to obtain information on API usage for a specific day. | 
| CaseSearch | search_cases | This endpoint retrieves cases according to keyword expressions you provide. | 
| CaseSearch | search_cases_by_id | Retrieve the search results corresponding to the specified caseSearchId value. | 
| CaseDocket | get_case | Retrieve the case with the specified caseId value. | 
| CaseDocket | get_case_parties | Retrieve the parties involved in the case with the specified caseId value. | 
| CaseDocket | get_case_attorneys | Retrieve the attorneys in the case with the specified caseId value. | 
| CaseDocket | get_case_judges | Retrieve the judges involved in the specified case. | 
| CaseDocket | get_case_docket_entries | Retrieve the docket entries in the case with the specified caseId value. | 
| CaseDocket | get_primary_documents_for_docket_entries | Retrieve the primary documents in the case with the specified caseId value. | 
| CaseDocket | get_secondary_documents_for_docket_entries | Retrieve the secondary documents in the case with the specified caseId value. | 
| CaseDocket | get_case_hearings | Gets Hearings for a requested Case ID. | 
| CaseDocket | get_case_related_cases | Retrieve cases that UniCourt has identified as related to the case with the specified caseId value. | 
| CaseDocket | get_party_by_id | Retrieve the party with the specified partyId value. | 
| CaseDocket | get_party_associated_attorneys | Retrieve the attorneys in the case with the specified partyId value. | 
| CaseDocket | get_attorney_by_id | Retrieve the attorney with the specified attorneyId value. | 
| CaseDocket | get_attorney_associated_parties | Retrieve the parties represented by the attorney with the specified attorneyId value. | 
| CaseDocket | get_judge_by_id | Retrieve the judge with the specified judgeId value. | 
| CaseDocuments | get_case_documents | Gets Documents for a requested Case ID. | 
| CaseDocuments | get_document_by_id | Gets details for a requested Document ID. | 
| CaseDocuments | get_case_document_download_by_id | Gets downloadable URL for a requested Document ID. | 
| CaseDocuments | order_case_document | Add Case Document Order for requested Document Ids. | 
| CaseDocuments | get_case_document_order_callbacks | Get Case Document Order Callback list for a requested Date. | 
| CaseDocuments | get_case_document_order_callback_by_id | Get Case Document Order Callback for a requested Case Document Order Callback Id. | 
| CaseUpdate | update_case | Request case updates for the specified case. | 
| CaseUpdate | get_case_updates | Retrieve case updates for the specified date. | 
| CaseUpdate | get_case_update_by_case_id | Retrieve case updates for the specified case object. | 
| CourtAvailability | get_court_coverage | Determine whether the specified court is covered by UniCourt. | 
| CaseTracking | track_case | Track the specified case. | 
| CaseTracking | get_case_tracks | Retrieve a list of all tracked cases. | 
| CaseTracking | get_case_track_by_id | Retrieve case tracking information for the specified caseId value. | 
| CaseTracking | remove_case_track_by_id | Remove Case Track for a specific Case Id. | 
| CaseExport | export_case | Retrieve information about the specified case export. | 
| CaseExport | get_case_export_callbacks | Retrieve callbacks according to the specified criteria. | 
| CaseExport | get_case_export_callback_by_id | Retrieve the specified case export callback object. | 
| PACERCredential | add_pacer_credential | Register PACER credentials with UniCourt. | 
| PACERCredential | get_pacer_credential | List registered PACER credentials. | 
| PACERCredential | get_pacer_credential_by_id | Retrieve the PACER credentials for the specified PACER username. | 
| PACERCredential | remove_pacer_credential_by_id | De-register the PACER credentials for the specified PACER username. | 
| PACER | import_pacer_case_by_court_using_case_number | Import the specified case from PACER.  | 
| PACER | all_courts_pacer_case_locator_case_search | Search all courts within the PACER system for a particular case. | 
| PACER | appeal_courts_pacer_case_locator_case_search | Search for PACER cases filed in U.S. Courts of Appeals. | 
| PACER | bankruptcy_courts_pacer_case_locator_case_search | Search for PACER cases filed in U.S. Bankruptcy Courts. | 
| PACER | civil_courts_pacer_case_locator_case_search | Search for civil cases filed in PACER. | 
| PACER | criminal_courts_pacer_case_locator_case_search | Search for criminal cases in PACER. | 
| PACER | multi_district_courts_pacer_case_locator_case_search | Search for multidistrict litigation in PACER. | 
| PACER | all_courts_pacer_case_locator_party_search | Search for the specified party across all PACER case filings. | 
| PACER | appeal_courts_pacer_case_locator_party_search | Search for the specified party across all PACER appeals cases. | 
| PACER | bankruptcy_courts_pacer_case_locator_party_search | Search for the specified party in PACER bankruptcy filings. | 
| PACER | civil_courts_pacer_case_locator_party_search | Search for the specified party in civil cases filed in PACER. | 
| PACER | criminal_courts_pacer_case_locator_party_search | Search for the specified party in PACER criminal cases. | 
| PACER | multi_district_courts_pacer_case_locator_party_search | Search for the specified party in multidistrict litigation in PACER. | 
| CourtStandards | get_courts | Retrieve information about a specified court or courts. | 
| CourtStandards | get_court | Retrieve information about a specified court. | 
| CourtStandards | get_court_locations_for_court | Retrieve the court locations associated with the specified court. | 
| CourtStandards | get_jurisdiction_geo_for_court | Retrieve the jurisdiction geography object for the specified court. | 
| CourtStandards | get_appeal_courts_for_court | Retrieve the appeals courts associated with the specified court. | 
| CourtStandards | get_court_types | Retrieve court types recognized by UniCourt. | 
| CourtStandards | get_court_type | Retrieve the information concerning the specific court type. | 
| CourtStandards | get_court_systems | Retrieve information about the specified court system or court systems. | 
| CourtStandards | get_court_system | Retrieve the specified court system. | 
| CourtStandards | get_court_locations | Retrieve the specified court location or court locations. | 
| CourtStandards | get_court_location | Contains the Court Location Object. | 
| CourtStandards | get_courts_for_court_location | Retrieve the courts associated with the specified court location. | 
| CourtStandards | get_jurisdictions_geo | Retrieve one or more jurisdiction geographies using a keyword expression. | 
| CourtStandards | get_jurisdiction_geo | Retrieve the specified jurisdiction geography. | 
| CourtStandards | get_courts_for_jurisdiction_geo | Returns Associated Court for given Jurisdiction Geo. | 
| CourtStandards | get_courts_service_status | Retrieve the status of one or more courts using a keyword expression. | 
| CourtStandards | get_court_service_status | Retrieve the court status of the specified court. | 
| CourtStandards | get_cases_class | Retrieve one or more case classes using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_case_class | Retrieve the specified case class. | 
| CourtStandards | get_areas_of_law | The keyword expression targeting the desired area of law.  | 
| CourtStandards | get_area_of_law | Retrieve the specified area of law. | 
| CourtStandards | get_case_type_groups | Retrieve one or more case type groups using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_case_type_group | Retrieve the specified case type group. | 
| CourtStandards | get_case_types | Retrieve one or more case types using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_case_type | Retrieve the specified case type. | 
| CourtStandards | get_charge_groups | Retrieve one or more charge groups using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_charge_group | Retrieve the specified charge group. | 
| CourtStandards | get_charges | Retrieve one or more charges using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_charge | Retrieve the specified charge. | 
| CourtStandards | get_charges_additional_data | Retrieve additional information on a charge using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_charge_additional_data | Retrieve the specified charge additional data. | 
| CourtStandards | get_charges_degree | Retrieve a charge degree using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_charge_degree | Retrieve the specified charge degree. | 
| CourtStandards | get_charges_severity | Retrieve a charge severity using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_charge_severity | Retrieve the specified charge severity. | 
| CourtStandards | get_causes_of_action_group | Retrieve a cause of action group using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_cause_of_action_group | Retrieve the specified cause of action group. | 
| CourtStandards | get_causes_of_action | Retrieve a cause of action using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_cause_of_action | Retrieve the specified cause of action. | 
| CourtStandards | get_causes_of_action_additional_data | Retrieve a cause of action additional data using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_cause_of_action_additional_data | Retrieve the specified cause of action additional data. | 
| CourtStandards | get_case_status_groups | Retrieve a case status group using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_case_status_group | Retrieve the specified case status group. | 
| CourtStandards | get_cases_status | Retrieve a case status using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_case_status | Retrieve the specified case status. | 
| CourtStandards | get_party_role_groups | Retrieve a party role group using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_party_role_group | Retrieve the specified party role group. | 
| CourtStandards | get_party_roles | Retrieve a party role using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_party_role | Retrieve the specified party role. | 
| CourtStandards | get_attorney_types | Retrieve an attorney type using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_attorney_type | Retrieve a specified attorney type object. | 
| CourtStandards | get_attorney_representation_types | Retrieve an attorney representation type using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_attorney_representation_type | Retrieve the specified attorney representation type. | 
| CourtStandards | get_judge_types | Retrieve a judge type using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_judge_type | Retrieve the specified judge type. | 
| CourtStandards | get_case_relationship_types | Retrieve an case relationship type using a keyword expression. Keyword expressions should be constructed according to the rules given above. | 
| CourtStandards | get_case_relationship_type | Retrieve the specified case relationship type. | 
| AttorneyAnalytics | search_normalized_attorneys | ### This endpoint retrieves information, including the normAttorneyId, on all attorneys in our normalized attorney database which match the request parameters. All query parameters supported by this API can be found in the schema section below. | 
| AttorneyAnalytics | search_normalized_attorneys_by_id | ### All query parameters supported for this API can be found in below schema section. Schema --> NormAttorneySearchQueryObject | 
| AttorneyAnalytics | get_norm_attorney_by_id | This endpoint retrieves information on the attorney in our normalized attorney database which matches the normAttorneyId specified in the request. | 
| AttorneyAnalytics | get_norm_judges_associated_with_norm_attorney | This endpoint returns information on all judges which have appeared in cases with the attorney specified by the normAttorneyId. The returned judges are ordered in descending order of number of cases shared with the relevant attorney. | 
| AttorneyAnalytics | get_norm_law_firms_associated_with_norm_attorney | Returns a list of Law Firms the norm Attorney has worked for. | 
| AttorneyAnalytics | get_norm_parties_associated_with_norm_attorney | Returns a list of Parties the Attorney has represented. | 
| CaseAnalytics | get_case_count_analytics_by_norm_attorney | Returns Case Analytics by Attorney. | 
| CaseAnalytics | get_case_count_analytics_by_opposing_norm_attorney_for_a_norm_attorney | Returns Case Analytics by Attorney. | 
| CaseAnalytics | get_case_count_analytics_by_norm_law_firm | Returns Case Analytics by Norm Law Firm. | 
| CaseAnalytics | get_case_count_analytics_by_opposing_norm_law_firm_for_a_norm_law_firm | Returns Case Analytics by Norm Law Firm. | 
| CaseAnalytics | get_case_count_analytics_by_norm_judge | Returns Case Analytics by Judge. | 
| CaseAnalytics | get_case_count_analytics_by_norm_party | Returns Case Analytics by Party. | 
| CaseAnalytics | get_case_count_analytics_by_opposing_norm_party_for_a_norm_party | Returns Case Analytics by Opposing Norm Party. | 
| CaseAnalytics | get_case_count_analytics_by_case_type | Get Case Count Analytics by Case Type. | 
| CaseAnalytics | get_case_count_analytics_by_area_of_law | Get Case Count Analytics by Area Of Law. | 
| CaseAnalytics | get_case_count_analytics_by_case_type_group | Get Analytics by Case Type Group. | 
| CaseAnalytics | get_case_count_analytics_by_case_class | Get Analytics by Case Class. | 
| CaseAnalytics | get_case_count_analytics_by_case_filed_date | Get Case Count Analytics grouped by Filing Date. | 
| CaseAnalytics | get_case_count_analytics_by_court | Get Case Count Analytics grouped by Court. | 
| CaseAnalytics | get_case_count_analytics_by_court_type | Get Case Count Analytics grouped by Court Type. | 
| CaseAnalytics | get_case_count_analytics_by_court_system | Get Case Count Analytics grouped by Court System. | 
| CaseAnalytics | get_case_count_analytics_by_court_location | Get Case Count Analytics grouped by Court Location. | 
| CaseAnalytics | get_case_count_analytics_by_jurisdiction_geo | Get Case Count Analytics grouped by Jurisdiction Geo. | 
| CaseAnalytics | get_case_count_analytics_by_party_role | Returns Case Analytics by Party Type. | 
| CaseAnalytics | get_case_count_analytics_by_party_role_group | Returns Case Analytics by Party Type Group. | 
| LawFirmAnalytics | search_normalized_law_firms | ### All query parameters supported for this API can be found in below schema section. Schema --> NormLawFirmSearchQueryObject | 
| LawFirmAnalytics | search_normalized_law_firms_by_id | ### All query parameters supported for this API can be found in below schema section. Schema --> NormLawFirmSearchQueryObject | 
| LawFirmAnalytics | get_norm_law_firm_by_id | The Law Firm API allows you to look up Law Firms by normLawFirmId. | 
| LawFirmAnalytics | get_norm_attorneys_associated_with_norm_law_firm | Returns a list of Attorneys associated to a Law Firm. | 
| LawFirmAnalytics | get_norm_judges_associated_with_norm_law_firm | Returns list of Judges faced by the Law Firm. | 
| LawFirmAnalytics | get_norm_parties_associated_with_norm_law_firm | Returns list of Parties represented by the Law Firm. | 
| JudgeAnalytics | search_normalized_judges | ### All query parameters supported for this API can be found in below schema section. Schema --> NormJudgeSearchQueryObject | 
| JudgeAnalytics | search_normalized_judges_by_id | ### All query parameters supported for this API can be found in below schema section. Schema --> NormJudgeSearchQueryObject | 
| JudgeAnalytics | get_norm_judge_by_id | The Judge API allows you to look up Judge Details by normJudgeId. | 
| JudgeAnalytics | get_norm_attorneys_associated_with_norm_judge | Returns a list of attorneys associated with a judge. | 
| JudgeAnalytics | get_norm_law_firms_associated_with_norm_judge | Returns a list of Law Firms a Judge has heard. | 
| JudgeAnalytics | get_norm_parties_associated_with_norm_judge | Returns a list of Parties A Judge has seen. | 
| PartyAnalytics | search_normalized_parties | ### All query parameters supported for this API can be found in below schema section. Schema --> NormPartySearchQueryObject | 
| PartyAnalytics | search_normalized_parties_by_id | ### All query parameters supported for this API can be found in below schema section. Schema --> NormPartySearchQueryObject | 
| PartyAnalytics | get_norm_party_by_id | The Party Details API allows you to look up Parties by normPartyId. | 
| PartyAnalytics | get_norm_attorneys_associated_with_norm_party | Returns a list of  Attorneys the Party has been represented by. | 
| PartyAnalytics | get_norm_judges_associated_with_norm_party | Returns a list of Judges the party has faced. | 
| PartyAnalytics | get_norm_law_firms_associated_with_norm_party | Returns a list of Law Firms the Party has been represented by. | 
| Callback | get_callbacks | Get list of callback types with count for a requested Date. | 
