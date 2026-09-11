# Contacts API Test Cases

## TC-001: Retrieve Contact by Valid ID

**Method:** GET  
**Endpoint:** `/contacts/{contactId}`

**Objective:**  
Verify that a valid contact ID returns the expected contact record.

**Preconditions:**
- Valid GoHighLevel access token
- Valid contact exists in the test account
- Correct API version header is included

**Request Setup:**
- Authorization: Bearer Token
- Header: `Version: v3`

**Steps:**
1. Send a GET request for an existing contact ID.
2. Verify the HTTP status code.
3. Review the response body.
4. Confirm the returned record matches the requested contact.

**Expected Result:**
- HTTP status code is `200 OK`
- Response body contains the requested contact record
- Returned contact data corresponds to the requested contact ID

**Actual Result:**
- HTTP status code returned `200 OK`
- Requested contact record was returned successfully

**Status:** PASS