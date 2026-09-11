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

## TC-002: Create Contact and Verify Persistence

**Objective:**  
Verify that a new contact can be created successfully and then retrieved by its returned contact ID.

**Preconditions:**
- Valid GoHighLevel access token
- Valid location ID
- Correct API version header is included

**Steps:**
1. Send a request to create a new QA contact.
2. Verify the contact creation response is successful.
3. Capture the contact ID returned in the response.
4. Send a request to retrieve the newly created contact by ID.
5. Verify the retrieval response returns `200 OK`.
6. Confirm the returned contact data matches the data submitted during creation.

**Expected Result:**
- Contact is created successfully.
- A valid contact ID is returned.
- The newly created contact can be retrieved using that ID.
- Retrieved data matches the submitted test data.

**Actual Result:**
- Contact was created successfully.
- A contact ID was returned.
- Retrieval request returned `200 OK`.
- Returned contact data matched the created QA contact.

**Status:** PASS