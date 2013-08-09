# flockChat Tutoral

## Requirements

* git - http://git-scm.com/
* NodeJS - http://nodejs.org
* NodeWebKit - https://github.com/rogerwang/node-webkit

## Step 1 - clone repository

``` sh
git clone https://github.com/twilson63/flockChat.git
cd flockChat
```

## Step 2 - Add window node to package.json

Edit package.json

``` json
{
	"window": {
	  "width": 600,
		"toolbar": true
	}
}
```


## step 3 - Add our app logic 

Edit app/controllers/main.js

``` js
var package = require('./package');
 // init chat item
$scope.chat = { nick: 'Anonymous'};
// get chats
var url = package.firebase;
$scope.chats = angularFire(url, $scope, 'chats', []);

$scope.add = function(chat) {
  chat.timestamp = new Date();
  $scope.chats.push(chat);
  // only keep 100 items
  if ($scope.chats.length > 99) { $scope.chats.splice(0,1); }
  	$scope.chat = { nick: chat.nick };
    angular.element('textarea').focus();

    var top = angular.element('li:last-child').offset().top - 100;
    angular.element('body,html').animate({ scrollTop: top }, 800);
  };

  $scope.$watch('chats', function() {
    var top = angular.element('li:last-child').offset().top - 100;
    angular.element('body,html').animate({ scrollTop: top }, 800);
  });
```
## step 4 - Add Firebase URL to package.json

```
"firebase": ""
```
``