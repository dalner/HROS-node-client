#Socket Connection Client API
Socket Connection Client API gives you an easy to use javascript function API calls to manage the underlying socket.io connections. It helps manage dropped socket connections, state changes and other diagnostic information. It will be extended to support other items as the node server development and its API progresses.


#Getting started
First install all dependencies using [npm](http://npmjs.org/): 
```bash
$ npm install
```

This will install all necessesary dependencies such as 
*    grunt
*    grunt-contrib-jshint
*    grunt-contrib-nodeunit
*    grunt-contrib-uglify

Following successful install, run grunt: 
```bash
$ grunt
```

This will build the minified API into the build folder and into the hello world folder. 


#Functions
First create a new object:
```js
var varName = new HROS_JS();
```
##"Public" Variables
*  ConnectionStatus
Returns an integer value "enum" of type ConnectedStates which is also a "public" variable. Its states are as follows:
	-  CONNECTED (0)
	-  DISCONNECTED (1)
	-  CONNECTING (2)
	-  FAILED (3)

```js
// get connection status
var status = varName.ConnectionStatus();

// compare connection status to "enum"
if(status === varName.ConnectedStates.DISCONNECTED)
```

*  CurrentAction **Partial Implementation**
	-  This will return what it is currently doing. As a partial implementation, it will only return a NOTHING state or WALKING state. The ACTION state needs to be implemented but there needs to be a communcation back as to when the action starts and stops. 

This also returns a "enum" of type ActionStates which have the following variables:
-  ACTION (0)
-  WALKING (1)
-  NOTHING (2)

```js
// get Current Action State
var CurrentActionState = varName.CurrentActionStatus()

// comparing action states
if(CurrentActionState === varName.ActionStates.WALKING)
```



##General/Options
*  Connect takes an ip address, and attempts to connect to it 10 times before it sets ConnectionStatus to a failed state. 
```js
varName.Connect('192.168.1.2');
```
*  Initialize servos
```js
varName.Initialize();
```
##Actions
*   Play action by name stored in nodeJS server (which links page # to name)
```js
varName.PlayAction('sit');
```
##Walk
*    Toggle walk, if walking, stop, otherwise start
	- Cannot start walking if in middle of action
	- Cannot do actions while walking
```js
varName.ToggleWalk();
```
*    Walk Position send x & y coordinates make robot walk forward, backward, left & right
	- Safely you can go from **+50 to -50** but the variables can range from **+255 to -255** however, the greater the value coordinates the faster the robot walks
```js
varName.WalkPosition(x,y);
```

##Diagnostics
Diagnostics is still a continued effort. While there are function placeholders here, they are currently unimplemented. However, once implemented, they will look something like this. 

##Servo Diagnostics **UNIMPLEMENTED**
This will likely return various states of the servos, such as ERROR, DISCONNECTED, STABLE, HOT etc.
```js
var servoValues = varName.CheckServos()
```

##Battery Levels **UNIMPLEMENTED**
Will return the level of battery in some integer form. Likely in a form of a percentage, mAH value or integer. 
```js
var servoValues = varName.BatteryLevel()
```


