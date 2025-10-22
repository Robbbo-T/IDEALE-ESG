# IDEALE-ESG Platform Schemas

This directory contains the primary data model schemas for the IDEALE-ESG platform. The schemas are defined using [JSON Schema](https://json-schema.org/) Draft 7 specification to ensure well-defined, validated, and self-documenting data structures.

## Schema Files

### 1. ESG Metric Schema (`esg_metric.v1.json`)

Defines the structure for Environmental, Social, and Governance (ESG) metrics.

**Key Properties:**
- `id`: Unique identifier for the metric
- `metricName`: Name of the ESG metric (e.g., "Carbon Emissions", "Employee Diversity")
- `category`: ESG category (Environmental, Social, or Governance)
- `value`: Numerical value of the metric
- `unit`: Unit of measurement
- `reportingPeriod`: Time period for the metric
- `companyId`: Reference to the company
- `verificationStatus`: Status of metric verification (Unverified, Internal Review, External Audit, Certified)

**Example Usage:**
```json
{
  "id": "carbon-footprint-2024-q1",
  "metricName": "Carbon Emissions",
  "category": "Environmental",
  "subcategory": "Climate Change",
  "value": 1250.5,
  "unit": "tonnes CO2e",
  "reportingPeriod": {
    "startDate": "2024-01-01",
    "endDate": "2024-03-31"
  },
  "companyId": "acme-corp",
  "dataSource": "Internal Systems",
  "verificationStatus": "External Audit",
  "targetValue": 1000.0
}
```

### 2. Company Profile Schema (`company_profile.v1.json`)

Defines the structure for company profile information in the IDEALE-ESG system.

**Key Properties:**
- `id`: Unique identifier for the company
- `name`: Legal name of the company
- `industry`: Primary industry sector
- `country`: Primary country of operation (ISO 3166-1 alpha-2 code)
- `headquarters`: Detailed headquarters location
- `identifiers`: Business identifiers (Tax ID, LEI, Ticker, ISIN)
- `esgReporting`: ESG reporting frameworks and cycle information
- `certifications`: ESG and sustainability certifications

**Example Usage:**
```json
{
  "id": "acme-corp",
  "name": "Acme Corporation",
  "tradingName": "ACME",
  "industry": "Energy",
  "subIndustry": "Renewable Energy",
  "country": "US",
  "headquarters": {
    "address": "123 Green Street",
    "city": "San Francisco",
    "state": "CA",
    "postalCode": "94102",
    "country": "US"
  },
  "identifiers": {
    "ticker": "ACME",
    "lei": "12345678901234567890"
  },
  "employeeCount": 5000,
  "foundedYear": 1995,
  "website": "https://www.acme.com",
  "esgReporting": {
    "frameworks": ["GRI", "TCFD"],
    "reportingCycle": "Annual",
    "lastReportDate": "2024-03-31"
  }
}
```

## Schema Versioning

All schemas follow semantic versioning:
- Format: `{schema_name}.v{major}.json`
- Example: `esg_metric.v1.json`, `company_profile.v1.json`
- Breaking changes increment the major version
- Backward-compatible changes can be documented in release notes

## Validation

These schemas can be used to validate JSON data using various tools and libraries:

### Node.js (with Ajv)
```javascript
const Ajv = require('ajv');
const ajv = new Ajv();
const schema = require('./esg_metric.v1.json');
const validate = ajv.compile(schema);
const valid = validate(data);
```

### Python (with jsonschema)
```python
import jsonschema
import json

with open('esg_metric.v1.json') as f:
    schema = json.load(f)

jsonschema.validate(instance=data, schema=schema)
```

## ESG Frameworks Supported

The schemas are designed to support multiple ESG reporting frameworks:
- **GRI**: Global Reporting Initiative
- **SASB**: Sustainability Accounting Standards Board
- **TCFD**: Task Force on Climate-related Financial Disclosures
- **CDP**: Carbon Disclosure Project
- **DJSI**: Dow Jones Sustainability Indices
- **UNGC**: United Nations Global Compact
- **IIRC**: International Integrated Reporting Council

## Contributing

When adding or modifying schemas:
1. Follow JSON Schema Draft 7 specification
2. Include comprehensive descriptions for all properties
3. Provide example values
4. Update this README with changes
5. Increment version number for breaking changes
6. Maintain backward compatibility when possible

## Links

- [JSON Schema Documentation](https://json-schema.org/)
- [JSON Schema Validator](https://www.jsonschemavalidator.net/)
- [ESG Reporting Standards](https://www.globalreporting.org/)
