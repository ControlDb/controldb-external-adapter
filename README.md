# ControlDB IPFS External Adapter

See [Install Locally](#install-locally) for a quickstart

## Input Params

- `endpoint`: The endpoint to use from the IPFS API
- `ipfs_host`: The Base URL of you IPFS host
- `starting_char`: Which character to start at for returning the string

Parameters from the IPFS API: 
```
  quiet: false,
  quieter: false,
  silent: false,
  progress: false,
  trickle: false,
  pin: false,
  file: false, // The location of the file you want to upload
  arg: false
```

## Example input

```
curl -X POST -H "content-type:application/json" "http://localhost:8080/" --data '{ "id": 0, "data": {"file":"./test/test.json"}}'
```

## Output

```json
{
  "jobRunID":0,
  "data":{
    "Name":"test.json",
    "Hash":"Qmd3zUksep8MQnjeSsXgEE4xa2DKgw48HJPjk5BiMDn1u7",
    "Size":"24",
    "result":"Qmd3zUksep8MQnjeSsXgEE4xa2DKgw48HJPjk5BiMDn1u7"
  },
  "result":"Qmd3zUksep8MQnjeSsXgEE4xa2DKgw48HJPjk5BiMDn1u7",
  "statusCode":200
}
```
or

## Example input

```bash
curl -X POST -H "content-type:application/json" "http://localhost:8080/" --data '{ "id": 0, "data": {"endpoint":"api/v0/cat", "arg":"Qmd3zUksep8MQnjeSsXgEE4xa2DKgw48HJPjk5BiMDn1u7"}}'
```

## Output

```json
{"jobRunID":0,"data":{"cat":"dog"},"statusCode":200}
```

## Example Input 

```bash
curl -X POST -H "content-type:application/json" "http://localhost--data '{ "id": 0, "data": {"text_for_file_name":"patrick.json", "text_for_file":"[\"dog\"]"}}'
```

## Output

```json
{"jobRunID":0,"data":{"Name":"patrick.json","Hash":"QmWk8NQVeoXyMizcxT3D2y85eFDQGQfmRvupCnni3nuS1q","Size":"15","result":"QmWk8NQVeoXyMizcxT3D2y85eFDQGQfmRvupCnni3nuS1q"},"result":"QmWk8NQVeoXyMizcxT3D2y85eFDQGQfmRvupCnni3nuS1q","statusCode":200}
```

## Install Locally

Install dependencies:

```bash
yarn
```

### Test

Run the local tests:

```bash
yarn test
```

Natively run the application (defaults to port 8080):

### Run

```bash
yarn start
```

## Call the external adapter/API server

```bash
curl -X POST -H "content-type:application/json" "http://localhost:8080/" --data '{ "id": 0, "data": {"file":"./test/test.json"}}'
```

## Docker

If you wish to use Docker to run the adapter, you can build the image by running the following command:

```bash
docker build . -t external-adapter
```

Then run it with:

```bash
docker run -p 8080:8080 -it external-adapter:latest
```

## Serverless hosts

After [installing locally](#install-locally):

### Create the zip

```bash
zip -r external-adapter.zip .
```


#### To Set Up an API Gateway (REST API)

If using a REST API Gateway, you will need to disable the Lambda proxy integration for Lambda-based adapter to function.

- Click Add Trigger
- Select API Gateway in Trigger configuration
- Under API, click Create an API
- Choose REST API
- Select the security for the API
- Click Add
- Click the API Gateway trigger
- Click the name of the trigger (this is a link, a new window opens)
- Click Integration Request
- Uncheck Use Lamba Proxy integration
- Click OK on the two dialogs
- Return to your function
- Remove the API Gateway and Save
- Click Add Trigger and use the same API Gateway
- Select the deployment stage and security
- Click Add


## Setting up the adapter
1. Configure the external adapter with the required parameters to fetch the data you need. This may include specifying the API endpoint, any required authentication, and the format of the data.

2. Deploy the external adapter to a publicly accessible location, such as a web server or cloud service. You can use Chainlink's external adapter CLI tool to simplify this process.

3. Create a Chainlink node and configure it to use the external adapter you just deployed. This involves defining the job that will use the adapter, specifying the input parameters, and linking the output to your smart contract.

4. Deploy your smart contract to the blockchain, and define the interface that will be used to interact with the Chainlink node.

5. Once everything is set up, you can trigger the smart contract to request the off-chain data, which will be fetched by the Chainlink node and passed back to the smart contract. The smart contract can then use the data to execute its logic.


