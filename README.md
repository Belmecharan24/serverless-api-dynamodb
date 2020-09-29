Serverless REST API

Structure
This service has a separate directory for all the todo operations. For each operation exactly one file exists e.g. todos/delete.py. In each of these files there is exactly one function defined.

The idea behind the todos directory is that in case you want to create a service containing multiple resources e.g. users, notes, comments you could do so in the same service. While this is certainly possible you might consider creating a separate service for each resource. It depends on the use-case and your preference.

Setup
npm install -g serverless
Deploy
In order to deploy the endpoint simply run

serverless deploy
The expected result should be similar to:

Serverless: Packaging service...
Serverless: Excluding development dependencies...
Serverless: Uploading CloudFormation file to S3...
Serverless: Uploading artifacts...
Serverless: Uploading service serverless-rest-api-with-dynamodb.zip file to S3 (6.62 KB)...
Serverless: Validating template...
Serverless: Updating Stack...
Serverless: Checking Stack update progress...
............................................
Serverless: Stack update finished...
Service Information
service: serverless-rest-api-with-dynamodb
stage: dev
region: us-east-1
stack: serverless-rest-api-with-dynamodb-dev
resources: 38
api keys:
  myFirstKey: PbTEYNWrHn7JjeB281s2c1IGzJ7GlogO5fKy6cB0
endpoints:
  POST - https://XXXXXXX.execute-api.us-east-1.amazonaws.com/dev/todos
  GET - https://XXXXXXX.execute-api.us-east-1.amazonaws.com/dev/todos
  GET - https://XXXXXXX.execute-api.us-east-1.amazonaws.com/dev/todos/{id}
  PUT - https://XXXXXXX.execute-api.us-east-1.amazonaws.com/dev/todos/{id}
  DELETE - https://XXXXXXX.execute-api.us-east-1.amazonaws.com/dev/todos/{id}
functions:
  create: serverless-rest-api-with-dynamodb-dev-create
  list: serverless-rest-api-with-dynamodb-dev-list
  get: serverless-rest-api-with-dynamodb-dev-get
  update: serverless-rest-api-with-dynamodb-dev-update
  delete: serverless-rest-api-with-dynamodb-dev-delete
layers:
  None
Serverless: Run the "serverless" command to setup monitoring, troubleshooting and testing.
Usage
You can create, retrieve, update, or delete todos with the following commands:

Create a Todo
curl -X POST https://XXXXXXX.execute-api.us-east-1.amazonaws.com/dev/todos --data '{ "text": "Learn Serverless" }'
No output

List all Todos
curl https://XXXXXXX.execute-api.us-east-1.amazonaws.com/dev/todos
Example output:

[{"text":"Deploy my first service","id":"ac90feaa11e6-9ede-afdfa051af86","checked":true,"updatedAt":1479139961304},{"text":"Learn Serverless","id":"206793aa11e6-9ede-afdfa051af86","createdAt":1479139943241,"checked":false,"updatedAt":1479139943241}]%
Get one Todo
# Replace the <id> part with a real id from your todos table
curl https://XXXXXXX.execute-api.us-east-1.amazonaws.com/dev/todos/<id>
Example Result:

{"text":"Learn Serverless","id":"ee6490d0-aa11e6-9ede-afdfa051af86","createdAt":1479138570824,"checked":false,"updatedAt":1479138570824}%
Update a Todo
# Replace the <id> part with a real id from your todos table
curl -X PUT https://XXXXXXX.execute-api.us-east-1.amazonaws.com/dev/todos/<id> --data '{ "text": "Learn Serverless", "checked": true }'
Example Result:

{"text":"Learn Serverless","id":"ee6490d0-aa11e6-9ede-afdfa051af86","createdAt":1479138570824,"checked":true,"updatedAt":1479138570824}%
Delete a Todo
# Replace the <id> part with a real id from your todos table
curl -X DELETE https://XXXXXXX.execute-api.us-east-1.amazonaws.com/dev/todos/<id>
