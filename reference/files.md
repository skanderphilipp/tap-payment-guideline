## Overview   [Skip link to Overview](https://developers.tap.company/reference/files\#overview)

The files API endpoint in Tap is used to upload files to the Tap server. This is typically used in the onboarding process for merchants, where the file IDs are required for creating a business account, uploading required documents such as ID, commercial registration license, and logo, and for other API requests.

## File Request Example   [Skip link to File Request Example](https://developers.tap.company/reference/files\#file-request-example)

To upload a file, a request of type multipart/form-data is required. The request must include the file to be uploaded, as well as the parameters for creating a file. These parameters are listed in the [File Body Request Table](https://ixlcfimy.readme.io/reference/files#file-body-request-table-multipartform-data).

After the file is uploaded, the response will include a file ID that can be used to reference the file in other API requests. It is important to note that there are limits to the file size and type that can be uploaded, and files that exceed these limits will not be accepted by the Tap server.

#### File Body Request Table (multipart/form-data)   [Skip link to File Body Request Table (multipart/form-data)](https://developers.tap.company/reference/files\#file-body-request-table-multipartform-data)

| Field Name | Field Type | Description | Data Format |
| --- | --- | --- | --- |
| `file` | file | _required_<br>The file to be uploaded. This should follow the specifications of RFC 2388 (which defines file transfers for the multipart/form-data protocol). | [file](https://ixlcfimy.readme.io/reference/files#file-format-table-possible-values) |
| `purpose` | string | _required_<br>The purpose of the file. Possible values are business\_icon, business\_logo, customer\_signature, dispute\_evidence, finance\_report\_run, identity\_document, pci\_document, sigma\_scheduled\_query, or tax\_document\_user\_upload, memorandum\_association, bank\_statement , bank\_certificate, article\_of\_association, commercial\_registration<br>For more details check [File Purpose](https://ixlcfimy.readme.io/reference/files#file-purpose-table) | Text |
| `title` | string | _required_<br>Title of the document | Text |
| `file_link_create` | boolean | _required_<br>Whether to create a public link for the newly created file | true/false |
| `expires_at` | timestamp | _required_<br>A future timestamp after which the link will no longer be usable.<br>( use millisecond formate) | millisecond |
| `file_link_meta_data` | object | _optional_<br>Set of key-value pairs that you can attach to an object. This can be useful for storing additional information about the object in a structured format. |  |

#### File Purpose Table   [Skip link to File Purpose Table](https://developers.tap.company/reference/files\#file-purpose-table)

| PURPOSE | SUPPORTED FILE FORMATS | DESCRIPTION | MAX SIZE |
| --- | --- | --- | --- |
| `business_logo` | A business logo. | GIF, JPEG, PNG | 512KB |
| `customer_signature` | A customer signature. | JPG, PNG | 4MB |
| `dispute_evidence` | Evidence to submit with a dispute response. | JPEG, PDF, PNG | 8MB |
| `identity_document` | A document to verify the identity of an account owner during account provisioning. | JPEG, PNG | < 10MB |
| `pci_document` | A self-assessment PCI questionnaire. | PDF | 16MB |
| `tax_document_user_upload` | A user-uploaded tax document.A user-uploaded tax document. | CSV, DOCX, JPG, PDF, PNG, XLS, XLSX, | 16MB |

#### File Format Table (Possible values)   [Skip link to File Format Table (Possible values)](https://developers.tap.company/reference/files\#file-format-table-possible-values)

| FILE FORMAT | MIME TYPE |
| --- | --- |
| CSV | text/csv |
| DOCX | application/vnd.openxmlformats-officedocument.wordprocessingml.documentapplication/vnd.openxmlformats-officedocument.wordprocessingml.document |
| GIF | image/gif |
| PNG | image/png |
| JPEG | image/jpeg |
| PDF | application/pdf |
| XLS | application/vnd.ms-excel |
| XLSX | application/vnd.openxmlformats-officedocument.spreadsheetml.sheet |

## File Response Example   [Skip link to File Response Example](https://developers.tap.company/reference/files\#file-response-example)

After uploading a file, the JSON response will be returned with the file id that is required in some APIs. In the following table, you will find the response details.

| Key | Value | Description |
| --- | --- | --- |
| `id` | string | _optional_<br>File id, Its unique ID provide by Tap |
| `object` | string | _optional_<br>Name of the object-"file" |
| `live_mode` | boolean | _optional_<br>Environment mode |
| `api_version` | string | _optional_<br>Tap API version |
| `feature_version` | string | _optional_<br>Tap API feature version |
| `created` | integer | _optional_<br>File created date and time, Measured in seconds since the Unix epoc |
| `filename` | string | _optional_<br>Name of the file |
| `purpose` | string | _optional_<br>Purpose or Identification of the file (Please check the table File Formate to know Possible values & MAX SIZE) |
| `size` | integer | _optional_<br>The size in bytes of the file |
| `title` | string | _optional_<br>A user friendly title for the file |
| `type` | string | _optional_<br>The type of the file returned (e.g., csv, pdf, jpg, or png). |
| `url` | string | _optional_<br>URL of the file |
| `links` | array\[object\] | _optional_<br>List of file links |

JSON

```rdmd-code lang-json theme-light
{
  "id": "file_641212279714869248",
  "object": "file",
  "live_mode": false,
  "api_version": "1.0",
  "feature_version": "1.0",
  "created": 1572947320,
  "filename": "8801760e0a28ae2105e4ada503e30b8c.jpg",
  "purpose": "identity_document",
  "size": 346827,
  "title": "test",
  "type": "jpg",
  "url": "/files/file_641212279714869248",
  "links": [\
    {\
      "id": "link_641212281036075008",\
      "object": "file_link",\
      "live_mode": true,\
      "api_version": "1.0",\
      "feature_version": "1.0",\
      "created": 1572947320,\
      "expired": false,\
      "expires_at": 1234567,\
      "metadata": {\
        "key1": "value1",\
        "key2": "value2"\
      },\
      "url": "/links/fl_test_641212281036075009"\
    }\
  ]
}

```