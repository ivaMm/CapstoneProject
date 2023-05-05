# Capstone Project


## I. Project description

This project ilustrate simple car repair workflow. Customer can propose car repair, cancel it and revise it.
Provider can reject it, specifying new description and price, or accept it, specifying payment due. 
If rejected, customer can revise it. Once proposal is accepted, it will be archived and a new contract CarRepair will be created.


## II. Project dependencies

The tech requisites for running this service are:
- DAML (SDK version 2.6.1)
- JDK 11 or greater
- Daml Studio (IDE for Daml), extension on top of VS Code (included in Daml SDK)

You can install all dependencies following [this guide](https://docs.daml.com/getting-started/installation.html)


## III. How to run the system

### Start Daml Studio
Start Daml Studio by running command `daml studio ` within the project folder. This command will start VS Code.

### Build
In order to compile project run `daml build ` within the project folder. This command will build project according to config file daml.yaml. In particular it will download and install Daml SDK version specified in it.

In order to clean project run `daml clean ` within the project folder.

### Daml Sandbox
You can start Sandbox ledger together with Navigator via a terminal window using Daml Assistant command `daml start`. The ledger will run in the background on port 6865.
To stop the service press 'Ctrl-C' in a terminal window.
To start only Canton Sandbox run command `daml sandbox `

### Daml Json API
The Json API is a RESTful service that provides all necessary interactions with the ledger (contract creation, choice exercises, queries and fetches). The easiest way to start it is to run the command:
```
daml start
```
This will start the JSON API on port 7575 and connect it to a ledger running on port 6865, it will also start Navigator.
To stop the service press 'Ctrl-C' in a terminal window.
The API requires a bearer token for authentication. To retrieve one, go to [jwt](https://jwt.io) to generate one with the following payload:
```
{
    "https://daml.com/ledger-api": {
        "ledgerId": "sandbox",
        "applicationId": "HTTP-JSON-API-Gateway",
        "actAs": ["<allocated_party_identifier>"]
    }
}
```
! First you will need to query for the allocated parties (as any party), and than copy "identifier" of a party to actAs given party. 
Party identifier also can be found in Navigator.

This token allows interaction with the JSON API, acting as the specified party.

### Daml Navigator
The Navigator is a React frontend application, for local use, included in the Daml SDK, that allows read/write operations on contracts, as an allocated party, to simplify use for non-technical persons.
Start this service together with Sandbox via a terminal window by typing `daml start`.
Command `daml start ` will build DAR files, start the sandbox, upload DAR files, run the init-script specified in daml config file, and launch Navigator. 
The Navigator web-app is automatically started in your browser. If it fails to start, open a browser window and point it to the Navigator URL.
When running daml start you will see the Navigator URL. By default it will be http://localhost:7500/.
Init-script (Test:setup) will allow you to login as Customer, Provider or Employee and to inspect templates and contracts, and exercise choices of which given party is controller.
To stop the service press 'Ctrl-C' in a terminal window.


## Testing
Testing relies on the Daml Script library. 
You can run scripts in Daml Studio. Just click on "Script results" and it should open table view in separate column. From there, you can include archived contracts in a view, and you can switch to transaction view.
Scripts you can also run using command `daml test `from project root. It will display test summary and coverage. 
