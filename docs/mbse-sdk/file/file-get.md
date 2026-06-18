# API Name

API Name: File – Get Content

---

# Overview

This API retrieves the content of a file from the end system.

MBSE Core uses this API to:

* Download file content for attached files
* Retrieve binary file data for synchronization
* Support file transfer between systems
* Stream file content directly without storing intermediate copies

Connector responsibility:

* Receive the `fileLocationUri`.
* Invoke the appropriate mechanism to obtain the file content from `fileLocationUri`.
* Return the content as an `InputStream`.
* Stream the file content.

This API is implemented as a pass-through operation.

---

## API URI

```bash
GET: /mbse/api/1.0/content
    ?projectId={projectId}
    &fileLocationUri={fileLocationUri}
```

---

## URI Parameters

| Name            | Mandatory | Type   | Description                                                 |
| --------------- | --------- | ------ | ----------------------------------------------------------- |
| projectId       | True      | String | ID of the project.                                          |
| fileLocationUri | True      | String | Content download URL or file path where the file is stored. |

---

## Connector Contract

Connector must implement:

```java
void getFileContent(String fileLocationUri)
```

### Method Behavior

* Accept `fileLocationUri` as input.
* Return the content as `InputStream` in the servlet response.


---

## Behavior Rules

1. `projectId` must be validated before retrieving content.
2. `fileLocationUri` must be present.
3. File content should be streamed directly whenever possible.
4. Avoid loading entire files into memory for large files.
5. If file cannot be found:

    * Return HTTP `404 Not Found`
6. If access is denied:

    * Return HTTP `404 Not Found`
7. If file retrieval fails:

    * Return HTTP `500 Internal Server Error`
8. Connector must close streams appropriately after transfer completion.

---

## Response Payload

### Success Response

Binary stream response.

Example:

```http
HTTP/1.1 200 OK
Content-Type: application/octet-stream
```

Response body:

```text
<binary file content>
```

---

## Response Headers

| Header              | Required | Description                             |
| ------------------- | -------- | --------------------------------------- |
| Content-Type        | False    | MIME type of file if available.         |
| Content-Length      | False    | File size in bytes.                     |

---

## Example Use Case

### Download File Content

```bash
GET /mbse/api/1.0/content?
projectId=123
&fileLocationUri=https://example.com/files/block-diagram.png
```

---

## Implementation Guidelines

* Do not transform or decode file bytes.
* Use streaming APIs where supported.
* Handle large files efficiently.
* Ensure streams are properly closed after transmission.

---