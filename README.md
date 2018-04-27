#Test
$npm run dev-test

#Set up the blockchain app

Make a directory for the project called sf-chain. Set up a project in node:
$ mkdir sf-chain
$ cd-chain
$ npm init -y

#Install nodemon as a development dependency. 
Nodemon is a node engine with a live development server.
$npm init -y
$ npm i nodemon --save-dev

#Install Jest as development dependency.
Jest finds files with a `test.js` extension. It's a test runner for JavaScript. 
$ npm i jest --save-dev

#Test blockchain
$ npm run test 

#Add the express module to create a Node API
$ npm i express --save

#GET blocks
$ npm run dev
Now open the Postman application. Hit localhost:3001, and notice the response.
You should find the array of blocks of the blockchain.

#Add a POST request
Enables users to add blocks to the chain. First install the bodyParser middleware to handle incoming json in express:
$ npm i body-parser --save

Re-open Postman. Open a tab for a new request. Make sure it’s a POST request. Select body → Raw → json/application. Write in the json to post.
```
{
"data": "foo"
}
```
Enter `localhost:3001/mine` for the endpoint. Send. See the newly posted block in the chain.

#Connect Peers
In one command line tab:
$  npm run dev

In another command line tab:
$ HTTP_PORT=3002 P2P_PORT=5002 PEERS=ws://localhost:5001 npm run dev

Expect ‘socket connected’ to print in both tabs.

In a third command line tab:
$ HTTP_PORT=3003 P2P_PORT=5003 PEERS=ws://localhost:5001,ws://localhost:5002 npm run dev

Expect ‘socket connected’ to be printed two times in each tab.

#Peer Messages
Kill all the running instances on the command line. Fire up one instance with
$ npm run dev

Grow this blockchain a little. Open Postman, and fire two post requests to the mine endpoint. The endpoint is `localhost:3001/mine`, and the Raw → Body → Type → application/json:
```{ “data”: “foo” }```
Send. Send.

Run a second instance in a second command line tab:
$ HTTP_PORT=3002 P2P_PORT=5002 PEERS=ws://localhost:5001 npm run dev

Observe the received message - the blockchain of the original instance.

#P2P
Install the Websocket module: `ws`. This will allow us to create real-time connections between multiple users of the blockchain:
$ npm i ws --save

#Sync Chain
Confirm the chain synchronization. Kill all the running instances on the command line. Fire up one instance with
$ npm run dev

Grow this blockchain a little. Open Postman, and fire two post requests to the mine endpoint. The endpoint is `localhost:3001/mine`, and the Raw → Body → Type → application/json:
```{ “data”: “foo” }```
Send. Send.

Run a second instance in a second command line tab:
$ HTTP_PORT=3002 P2P_PORT=5002 PEERS=ws://localhost:5001 npm run dev

Hit `localhost:3002/blocks`. Notice the synchronization.

Check that the post method also synchronization. Add a new block, with `localhost:3001/mine`:
Hit localhost:3001/mine

Now `localhost:3002/blocks` and `localhost:3002/blocks` should return the same chain.





