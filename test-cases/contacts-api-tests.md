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
- HTTP status code is `200 OK`.
- Response body contains the requested contact record.
- Returned contact data corresponds to the requested contact ID.

**Actual Result:**
- HTTP status code returned `200 OK`.
- Requested contact record was returned successfully.

**Status:** PASS


## TC-002: Create Contact and Verify Persistence

**Method:** POST, followed by GET verification  
**Endpoint:** `/contacts/`, followed by `/contacts/{contactId}`

**Objective:**  
Verify that a new contact can be created successfully and then retrieved by its returned contact ID.

**Preconditions:**
- Valid GoHighLevel access token
- Valid location ID
- Correct API version header is included

**Request Setup:**
- Authorization: Bearer Token
- Header: `Version: v3`
- Request body includes valid contact data and location ID

**Steps:**
1. Send a POST request to create a new QA contact.
2. Verify the contact creation response is successful.
3. Capture the contact ID returned in the response.
4. Send a GET request to retrieve the newly created contact by ID.
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

**Method:** PUT, followed by GET verification  
**Endpoint:** `/contacts/{contactId}`

**Objective:**  
Verify that updating selected contact fields changes only the submitted fields and preserves existing contact data that was not included in the request.

**Preconditions:**
- Existing QA contact
- Valid GoHighLevel access token
- Correct API version header is included

**Request Setup:**
- Authorization: Bearer Token
- Header: `Version: v3`
- Request body includes updated first and last name only

**Steps:**
1. Send a PUT request for an existing contact.
2. Change the contact's first and last name.
3. Do not include the existing email address in the request body.
4. Verify the update request returns `200 OK`.
5. Send a GET request to retrieve the contact again by ID.
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


## TC-004: Delete Contact and Verify Removal

**Method:** DELETE, followed by GET verification  
**Endpoint:** `/contacts/{contactId}`

**Objective:**  
Verify that an existing contact can be deleted successfully and is no longer retrievable afterward.

**Preconditions:**
- Existing QA contact
- Valid GoHighLevel access token
- Correct API version header is included

**Request Setup:**
- Authorization: Bearer Token
- Header: `Version: v3`

**Steps:**
1. Send a DELETE request for an existing contact.
2. Verify the delete request returns a successful response.
3. Send a GET request using the same contact ID.
4. Verify the deleted contact is no longer returned.
5. Confirm the contact is no longer visible in the GoHighLevel UI.

**Expected Result:**
- Delete request succeeds.
- Deleted contact cannot be retrieved afterward.
- API returns an appropriate contact-not-found response.
- Contact is no longer present in the GoHighLevel UI.

**Actual Result:**
- Delete request returned `200 OK`.
- Follow-up retrieval returned `400 Bad Request` with a contact-not-found response.
- Contact was confirmed absent from the GoHighLevel UI.

**Status:** PASS


## TC-005: Retrieve Contact Using Invalid ID

**Method:** GET  
**Endpoint:** `/contacts/{invalidContactId}`

**Objective:**  
Verify that the API returns an appropriate error when a contact is requested using an invalid contact ID.

**Preconditions:**
- Valid GoHighLevel access token
- Correct API version header is included

**Request Setup:**
- Authorization: Bearer Token
- Header: `Version: v3`
- Invalid contact ID is used in the endpoint

**Steps:**
1. Send a GET request using an invalid contact ID.
2. Review the HTTP status code.
3. Review the error response.

**Expected Result:**
- API rejects the request.
- Response indicates that the contact could not be found.

**Actual Result:**
- API returned `400 Bad Request`.
- Response indicated that the contact was not found.

**Status:** PASS


## TC-006: Retrieve Contact Without Authentication

**Method:** GET  
**Endpoint:** `/contacts/{contactId}`

**Objective:**  
Verify that the API rejects a contact retrieval request when no authorization token is provided.

**Preconditions:**
- Valid contact ID
- Correct API version header is included

**Request Setup:**
- Authorization: None
- Header: `Version: v3`

**Steps:**
1. Send a GET request using a valid contact ID.
2. Do not include an Authorization header.
3. Keep the `Version: v3` header included.
4. Review the HTTP status code.
5. Review the error response.

**Expected Result:**
- API returns `401 Unauthorized`.
- Response indicates that authentication is required or missing.

**Actual Result:**
- API returned `401 Unauthorized`.
- Response message: `No Authorization header found for authentication!`

**Status:** PASS


## TC-007: Retrieve Contact Without Version Header

**Method:** GET  
**Endpoint:** `/contacts/{contactId}`

**Objective:**  
Verify that the API rejects a contact retrieval request when the required version header is missing.

**Preconditions:**
- Valid GoHighLevel access token
- Valid contact ID

**Request Setup:**
- Authorization: Bearer Token
- `Version` header omitted

**Steps:**
1. Send a GET request using a valid contact ID.
2. Include a valid Authorization header.
3. Do not include the `Version` header.
4. Review the HTTP status code.
5. Review the error response.

**Expected Result:**
- API rejects the request.
- Response indicates that the required version header is missing.

**Actual Result:**
- API returned `401 Unauthorized`.
- Response message: `version header was not found.`

**Status:** PASS

## TC-008: Create Contact Without Location ID

**Method:** POST  
**Endpoint:** `/contacts/`

**Objective:**  
Verify that the API rejects a contact creation request when the required location ID is omitted.

**Preconditions:**
- Valid GoHighLevel access token
- Correct API version header is included

**Request Setup:**
- Authorization: Bearer Token
- Header: `Version: v3`
- Request body contains valid contact data
- `locationId` is omitted from the request body

**Steps:**
1. Send a POST request to create a new contact.
2. Do not include `locationId` in the request body.
3. Review the HTTP status code.
4. Review the error response.

**Expected Result:**
- API rejects the request.
- Response indicates that valid location context is required.

**Actual Result:**
- API returned `403 Forbidden`.
- Response message: `The token does not have access to this location.`

**Status:** PASS

