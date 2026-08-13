## Overview

Tools are the external integrations and utility functions the TestGen Agent uses to communicate with JIRA, process data, and export results. Each tool has a defined interface, authentication method, error behavior, and example usage.

---

## Tool Index

| ID     | Tool Name             | Type        | Direction | Description                                      |
|--------|-----------------------|-------------|-----------|--------------------------------------------------|
| TL-01  | `jira_fetch_issue`    | REST API    | Inbound   | Fetch a single JIRA issue by key                 |
| TL-02  | `jira_search_issues`  | REST API    | Inbound   | Search issues using JQL query                    |
| TL-03  | `jira_fetch_comments` | REST API    | Inbound   | Retrieve all comments on a JIRA issue            |
| TL-04  | `jira_create_issue`   | REST API    | Outbound  | Create a test case sub-task back in JIRA         |
| TL-05  | `jira_add_comment`    | REST API    | Outbound  | Post generated test cases as a JIRA comment      |
| TL-06  | `jira_get_sprints`    | REST API    | Inbound   | List active sprints for a board                  |
| TL-07  | `file_exporter`       | Utility     | Outbound  | Write test cases to .md / .json / .csv / .xml    |
| TL-08  | `webhook_receiver`    | Webhook     | Inbound   | Receive JIRA issue-created / updated events      |
| TL-09  | `nlp_extractor`       | AI/LLM      | Internal  | NLP-based extraction for unstructured text       |
| TL-10  | `xray_importer`       | REST API    | Outbound  | Push test cases to JIRA XRAY test management     |

---

## Authentication

All JIRA tools use **HTTP Basic Auth** with an API token.

```bash
# Environment variables required
export JIRA_BASE_URL="https://sathish-kumar-elangovan.atlassian.net/browse/KAN-3"
export JIRA_EMAIL="esathishkumar16@gmail.com"
export JIRA_API_TOKEN="ATATT3xFfGF0IXuCAw9MHWCMrzro_XABNgPQ7_jXweiOte8J-MsYSFhn39BMpq-mvRhKirZOQljnB278MTBi2C_Ik4iUqZeGFPQb4kyakpbkhD8Q3_7ns70eHNWHHRNn6pgYmtq9-4ISIGt8igX5bmdgdgsRi1A7-13fPUMpIRdnkoHUz8Ua2MY=85409275"
```

**Authorization header:**
```
Authorization: Basic base64(EMAIL:API_TOKEN)
Content-Type: application/json
```

**How to generate an API token:**
1. Go to https://id.atlassian.com/manage-profile/security/api-tokens
2. Click "Create API token"
3. Copy and store securely in environment variables

---

**Output paths produced:**

| Format     | Example Output File                    |
|------------|----------------------------------------|
| Markdown   | `./output/PROJ-123-tests.md`           |
| JSON       | `./output/PROJ-123-tests.json`         |
| CSV        | `./output/PROJ-123-tests.csv`          |
| XRAY XML   | `./output/PROJ-123-tests.xml`          |

**CSV column order:**
```
TC ID | Title | Type | Priority | Preconditions | Steps | Expected Result | Traceability | Gherkin
```

---

