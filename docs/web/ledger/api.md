#### Artifact Family
----

An artifact represents an item of evidence. Typically an artifact is a single document (e.g., notice file, source code archive, bill of materials). An envelope is a special instance of an artifact which represents a collection of artifacts potentially including  other envelopes. For single artifacts the artifact_list field will be empty. For an envelope it will contain a list of zero of more artifacts and the content_type field will be set to "envelope". The uri_list field is a list because copies of the artifact could exist in multiple locations.


#### Artifact Create

```
POST /ledger/api/v1.1/artifacts
```

Allows the user to create an artifact into the sPart ledger. The request must be performed by a user with roles: "admin" or "member".

<table>
    <thead>
        <tr>
            <th>Field</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>uuid</td>
            <td>string</td>
            <td>unique identifier</td>
        </tr>
        <tr>
            <td>name</td>
            <td>string</td>
            <td>file or envelope name</td>
        </tr>
        <tr>
            <td>alias (was short_id)</td>
            <td>string</td>
            <td>alias for typing</td>
        </tr>
        <tr>
            <td>label</td>
            <td>string</td>
            <td>// Display name</td>
        </tr>
        <tr>
            <td>checksum</td>
            <td>string</td>
            <td>artifact checksum</td>
        </tr>
        <tr>
            <td>openchain</td>
            <td>string</td>
            <td>true/false If prepared under an OpenChain comforting program</td>
        </tr>
        <tr>
            <td>content_type</td>
            <td>string</td>
            <td>envelope, notices, spdx, source, ...</td>
        </tr>
    </tbody>
</table>

Example of single artifact request:

```
{
   private_key: "5K9ft3F4CDHMdGbeUZSyt77b1TJavfR7CAEgDZ7nXbdno1aynbt",
   public_key: "034408551a7b24b917103ccfafb402195713cd2e5dcdc588e7dc537f07b195bcf9",
   artifact: {	
		uuid: "7709ca8d-01f4-4de2-69ed-16b7ebae704a",
	  	name: "Zephypr 1.12 SPDX file",
	  	alias: "zephypr_1.12",
	  	label: "Zephypr 1.12 SPDX file",
	  	checksum: "f855d41c49e80b9d6f2a13148e5eb838607e92f1",
	  	openchain: true,
	  	content_type: "spdx"
	}
}
```

Example of curl request:

```
curl -i -H "Content-Type: application/json" -X POST -d  '{"private_key": "5K92SiHianMJRtqRiMaQ6xwzuYz7xaFRa2C8ruBQT6edSBg87Kq", "public_key" : "02be88bd24003b714a731566e45d24bf68f89ede629ae6f0aa5ce33baddc2a0515", "artifact": {"uuid": "7709ca8d-01f4-4de2-69ed-16b7ebae705c","name": "Zephypr 1.12 SPDX file", "checksum": "f855d41c49e80b9d6f2a13148e5eb838607e92f1", "alias": "zephypr_1.12", "label": "Zephypr 1.12 SPDX file", "openchain": "true", "content_type": "spdx"} }' http://147.11.176.111:818/ledger/api/v1.1/artifacts
```

**Potential Errors**:

- The requesting user does not have the appropriate access credentials to perform the create.
- One or more of the required fields are missing.
- The UUID is not in a valid format. 
- The UUID is not unique to the artifact.


#### Artifact Amend

```
POST /ledger/api/v1.1/artifacts/amend
```

Allows the user to amend an artifact in the sPart ledger. The request must be performed by a user with roles: "admin" or "member".

<table>
    <thead>
        <tr>
            <th>Field</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>uuid</td>
            <td>string</td>
            <td>unique identifier</td>
        </tr>
        <tr>
            <td>name</td>
            <td>string</td>
            <td>file or envelope name</td>
        </tr>
        <tr>
            <td>alias (was short_id)</td>
            <td>string</td>
            <td>alias for typing</td>
        </tr>
        <tr>
            <td>label</td>
            <td>string</td>
            <td>// Display name</td>
        </tr>
        <tr>
            <td>checksum</td>
            <td>string</td>
            <td>artifact checksum</td>
        </tr>
        <tr>
            <td>openchain</td>
            <td>string</td>
            <td>true/false If prepared under an OpenChain comforting program</td>
        </tr>
        <tr>
            <td>content_type</td>
            <td>string</td>
            <td>envelope, notices, spdx, source, ...</td>
        </tr>
    </tbody>
</table>

Example of single artifact request:

```
{
   private_key: "5K9ft3F4CDHMdGbeUZSyt77b1TJavfR7CAEgDZ7nXbdno1aynbt",
   public_key: "034408551a7b24b917103ccfafb402195713cd2e5dcdc588e7dc537f07b195bcf9",
   artifact: {	
		uuid: "7709ca8d-01f4-4de2-69ed-16b7ebae704a",
	  	name: "Zephypr 1.12 SPDX file",
	  	alias: "zephypr_1.12",
	  	label: "Zephypr 1.12 SPDX file",
	  	checksum: "f855d41c49e80b9d6f2a13148e5eb838607e92f1",
	  	openchain: true,
	  	content_type: "spdx"
	}
}

	or

{
   private_key: "5K9ft3F4CDHMdGbeUZSyt77b1TJavfR7CAEgDZ7nXbdno1aynbt",
   public_key: "034408551a7b24b917103ccfafb402195713cd2e5dcdc588e7dc537f07b195bcf9",
   artifact: {	
		uuid: "7709ca8d-01f4-4de2-69ed-16b7ebae704a",
	  	name: "Zephypr 1.12 SPDX file",
	  	alias: "zephypr_1.12"
	}
}
```

(Note: The payload is valid as long as "private_key", "public_key", "artifact" and "uuid" are present.)

Example curl request:

```
curl -i -H "Content-Type: application/json" -X POST -d  '{"private_key": "5K92SiHianMJRtqRiMaQ6xwzuYz7xaFRa2C8ruBQT6edSBg87Kq", "public_key" : "02be88bd24003b714a731566e45d24bf68f89ede629ae6f0aa5ce33baddc2a0515", "artifact": {"uuid": "7709ca8d-01f4-4de2-69ed-16b7ebae705c","name": "Zephypr 1.12 SPDX file", "checksum": "f855d41c49e80b9d6f2a13148e5eb838607e92f1", "alias": "zephypr_1.12", "label": "Zephypr 1.12 SPDX file", "openchain": "true", "content_type": "spdx"} }' http://147.11.176.111:818/ledger/api/v1.1/artifacts/amend

	or

curl -i -H "Content-Type: application/json" -X POST -d  '{"private_key": "5K92SiHianMJRtqRiMaQ6xwzuYz7xaFRa2C8ruBQT6edSBg87Kq", "public_key" : "02be88bd24003b714a731566e45d24bf68f89ede629ae6f0aa5ce33baddc2a0515", "artifact": {"uuid": "7709ca8d-01f4-4de2-69ed-16b7ebae705c","name": "Zephypr 1.12 SPDX file", "checksum": "f855d41c49e80b9d6f2a13148e5eb838607e92f1", "alias": "zephypr_1.12"} }' http://147.11.176.111:818/ledger/api/v1.1/artifacts/amend
```

**Potential Errors**:

- The requesting user does not have the appropriate access credentials to perform the create.
- No fields were amended.
- The UUID is not in a valid format. 
- The UUID does not exist.


#### Artifact List

```
GET /ledger/api/v1.1/artifacts
```

Allows the user to obtain a list of artifact from the sPart ledger. This is a public function.

Example of list artifact response:

```
{
    status:     "success",
    message:    "OK",
    result_type: "ArtifactRecord",
    result: [
        {
            ...
        },
        {
            ...
        },
        {
            ...
        }
    ]
}
```

IF there are not artifacts registered, then an empty list will be returned as shown:

```
{   
    status:     "success",
    message:    "OK",
    result_type: "ListOf:ArtifactRecord",
    result:     []
}
```

**Potential Errors**:

- Data cannot be deserialized due to encoding error.


#### Artifact Retrieve

```
GET /ledger/api/v1.1/artifacts/{uuid}
```

Allows the user to obtain the artifact data associating with the uuid from the sPart ledger. This is a public function.

Example of a <u>single</u> artifact response:

```
{	
	status: 	"success",
	message: 	"OK",
	result_type: "ArtifactRecord",
	result: {
		name: "Zephyr 1.12 Notice File",
		uuid: "26559ed4-6868-488d-a5a7-3e81714beb00",
		checksum: "f855d41c49e80b9d6f2a13148e5eb838607e92f1",
		content_type: "notices",
		alias: "zephyr-notices-1.12",
		label: "Zephyr Notices 1.12",
		openchain: "True",
		timestamp: "2018-06-18 00:30:12.498167"
		artifact_list: []   /* not used for singular artifact */
		uri_list: [ 
			{
				version: "1.0",
		   		alias: "zephyr-notices-1.12",
			   	checksum: "Zephyr Notices 1.12",
			   	size:	"235120"
			   	content_type: "http",
			   	location: "https://...."
			}
		]
	}
}
```

Example of an <u>envelope</u> response:

```
{	
	status: 	"success",
	message: 	"OK",
	result_type: "ArtifactRecord",
	result: {   
		name: "Zephyr 1.12 Envelope",
		uuid: "9b602058-c73f-4f02-9237-b71a2760fc15",
		checksum: "a1e2486417f4cd7fc670bf5facd5870af9c1e3a5",
		content_type: "envelope",
		alias: "zephyr-notices-1.12",
		label: "Zephyr Notices 1.12",
		openchain: "True",
		timestamp: "2018-06-18 00:30:12.498167"
		artifact_list: [
    		{
    			uuid: "731ef148-5f81-11e8-9c2d-fa7ae01bbebc",
            	path: "/spdx"
    		},
			{
				uuid: "f2cef148-5f81-11e8-8f51-fa7ae01bb93b",
			    path: "/notices"
			}
		] 
		uri_list: [ 
			{
    			version: "1.0",
				alias: "zephyr-envelope-1.12",
				checksum: "f67d3213907a52012a4367d8ad4f093b65abc016",
				size:	"235120"
				content_type: "http",
				location: "https://...."
			}
		]
	}
}
```

Note that the envelope record utilizes the artifact_list field where a single artifact does not.

**Potential Errors**:

- The UUID does not exist.


#### Artifact Retrieve History

```
GET /ledger/api/v1.1/artifacts/history/{uuid}
```

Allows the user to obtain the historical data of an artifact associating with the uuid from the sPart ledger. This is a public function.

Example of historical artifact response:

```
Sample goes here
```

**Potential Errors**:

- The UUID does not exist.


#### Artifact Retrieve Range

```
GET /ledger/api/v1.1/artifacts/{uuid}/date/{yyyymmdd}
```

Allows the user to obtain the artifact data associating with the uuid given a specific date from the sPart ledger. This is a public function and it returns the state which is most relevant to the given date.

Example of range artifact response:

```
Sample goes here
```

**Potential Errors**:

- The UUID does not exist.

