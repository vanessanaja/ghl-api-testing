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

## TC-003: Update Contact and Verify Existing Data Is Preserved

**Objective:**  
Verify that updating selected contact fields changes only the submitted fields and preserves existing contact data that was not included in the request.

**Preconditions:**
- Existing QA contact
- Valid GoHighLevel access token
- Correct API version header is included

**Steps:**
1. Send an update request for an existing contact.
2. Change the contact's first and last name.
3. Do not include the existing email address in the request body.
4. Verify the update request returns `200 OK`.
5. Retrieve the contact again by ID.
6. Confirm the updated name values are present.
7. Confirm the existing email address remains unchanged.
8. Confirm the changes are reflected in the GoHighLevel UI.

**Expected Result:**
- Update request returns `200 OK`.
- Submitted name fields are updated.
- Existing email remains unchanged.
- Retrieved API data matches the updated contact record.
- GoHighLevel UI reflects the same changes.

**Actual Result:**
- Update request returned `200 OK`.
- First and last name were updated successfully.
- Existing email remained unchanged.
- Retrieval request returned `200 OK`.
- Updated values were confirmed in both Postman and GoHighLevel.

**Status:** PASS