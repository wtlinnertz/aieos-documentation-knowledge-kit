# API Reference Record

---

## 1. Document Control

| Field | Value |
|-------|-------|
| ARR ID | ARR-{PROJECT}-{NNN} |
| System Name | {system name} |
| Owner | {team or role — not an individual person} |
| Version | v{N} |
| Status | Draft / Validated / Freeze Pending / Frozen |
| TDD Reference | {TDD-{PROJECT}-{NNN}} |
| API Version | {API version being documented} |
| Governance Model Version | 1.0 |
| Prompt Version | {prompt version} |
| Spec Version | {spec version} |
| Principles Version | {principles file versions} |

---

## 2. API Overview

**Purpose:** {brief description of the API's purpose and scope}

**Base URL:** {base URL pattern or convention, e.g., `https://api.example.com/v1`}

**Supported Content Types:** {e.g., `application/json`}

**Rate Limiting:** {rate limiting policy, or "None"}

### Endpoint Summary

| Method | Path | Description |
|--------|------|-------------|
| {GET/POST/...} | {/path} | {brief description} |
| {GET/POST/...} | {/path} | {brief description} |

*List every public endpoint as a summary.*

---

## 3. Authentication

**Method:** {e.g., API Key, OAuth 2.0, JWT, Session Token}

**Obtaining Credentials:** {how to obtain credentials}

**Including Credentials in Requests:**
{how to include credentials — header name, format, example}

**Per-Endpoint Overrides:**
{list any endpoints with different auth requirements, or "All endpoints use the global authentication model"}

**Unauthenticated Endpoints:**
{list endpoints requiring no authentication, or "All endpoints require authentication"}

---

## 4. Endpoint Documentation

### 4.1 {Endpoint Name}

| Field | Value |
|-------|-------|
| Method | {GET / POST / PUT / DELETE / PATCH} |
| Path | {/path/to/resource} |
| Description | {what this endpoint does} |
| Authentication | {auth requirement or "Global"} |

**Parameters:**

| Name | Location | Type | Required | Description | Constraints |
|------|----------|------|----------|-------------|-------------|
| {name} | {path / query / header} | {type} | {Yes / No} | {description} | {constraints, if any} |

**Request Body:** {if applicable}

```json
{
  "field": "type — description"
}
```

**Response (Success):**

| Status Code | Description |
|-------------|-------------|
| {200/201/...} | {description} |

```json
{
  "field": "type — description"
}
```

**Error Responses:**

| Status Code | Error | Description |
|-------------|-------|-------------|
| {400/401/...} | {error name} | {when this error occurs} |

**Example:**

Request:
```
{METHOD} {/path} HTTP/1.1
{headers}

{request body if applicable}
```

Response:
```json
{response body}
```

### 4.2 {Endpoint Name}

*Repeat the structure above for every public endpoint.*

*Every public endpoint from the TDD must appear here.*

---

## 5. Error Reference

### Common Error Response Format

```json
{
  "error": {
    "code": "{error_code}",
    "message": "{human-readable message}",
    "details": "{additional context, if any}"
  }
}
```

### Error Code Catalogue

| Status Code | Error Name | Description | When It Occurs |
|-------------|-----------|-------------|----------------|
| {400} | {Bad Request} | {description} | {when this error occurs} |
| {401} | {Unauthorized} | {description} | {when this error occurs} |
| {403} | {Forbidden} | {description} | {when this error occurs} |
| {404} | {Not Found} | {description} | {when this error occurs} |
| {500} | {Internal Server Error} | {description} | {when this error occurs} |

*Include every error status code used across all endpoints.*

---

## 6. Versioning and Deprecation

| Field | Value |
|-------|-------|
| Current API Version | {version} |
| Versioning Mechanism | {how versioning works — URL path, header, query parameter} |

**Deprecation Policy:** {how deprecation is communicated, timeline, what happens to deprecated endpoints — or "No deprecation policy established"}

**Changelog:**
{changelog for the current version, or link to changelog location}
