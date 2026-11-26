# FHIR HAPI Validation

Validates the public HAPI FHIR R4 server:
https://hapi.fhir.org/baseR4

## Requirements
- Node.js and npm
- Newman: npm install -g newman

## Run
From the postman directory:

newman run FHIR_HAPI_Validation.postman_collection.json -e FHIR_HAPI_Env.postman_environment.json -d resources.csv --reporters "cli,json" --reporter-json-export newman_report.json

## What each request checks
01 - Metadata: FHIR R4 version, starter resource support, and advertised Patient _lastUpdated support.
02 - Sample: searchset Bundle, page-size limit, resource type, IDs, timestamps, and unique IDs within the page.
03 - Count: successful response with a numeric total.
04 - Incremental: returned records are newer than the input watermark and sorted by lastUpdated.
05 - Paging: follows the next link from request 04 and checks the returned Bundle.

## Test data
resources.csv provides six resource types and their watermark timestamps.
Each row runs the entire collection once.

## Results
Terminal output shows pass/fail results.
newman_report.json stores the detailed run report.
The CSV is input only and is not modified.

The public server's data and availability may change.