# InpediaClientService
The front facing REST service to which all clients will talk to regarding add/update/delete of their indices. This service is meant to be used by different language integrations of Inpedia.
This service does NOT provide the facility to perform a search.

## Reference
Each request to this service is called a `task`. A single `task` should be directed to a single search `index` for the client. Each modification (add, update, delete) is represented by a `sub_task`.
One `task` can result in update, delete and addition of objects within that `index` only.

## API
All requests should be sent to the endpoint `/clients/task` with the `POST` HTTP verb.
The request body may contain the following parameters:

| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `clientId` | `String` | **Required** The Client Id provided by Inpedia |
| `token` | `String` | **Required** The security token to be validated by Inpedia Auth Server |
| `index` | `String` | **Required** The index for which the `task` is meant for |
| `batchUpdate` | `boolean` | **Optional** Whether the update is to be updated as a single batch. Even if one `sub_task` fails, entire request fails |
| `data` | `Array` | **Required** The array of `sub_task`s |

Each `sub_task` contains the following parameters:

| Parameter | Type | Description |
| --------- | ----- | ---------- |
| `_operation` | `String` | **Required** The type of operation, `add` or `update` or `delete` |
| `data` | `Object` | **Required** The object over which the operation is to be performed |
