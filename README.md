sfTypeahead: A Twitter Typeahead directive
=================

A simple Angular.js directive wrapper around the Twitter Typeahead library.

License: [MIT](http://www.opensource.org/licenses/mit-license.php)

Getting Started
---------------

How you acquire angular-typeahead is up to you.

Preferred method:
* Install with [Bower][bower]: `$ bower install https://github.com/Causemap/angular-typeahead.git#`

**Note:** angular-typeahead.js has dependencies on the following libraries:
* [typeahead.js][typeahead.js] v0.10.x
* [bloodhound.js][typeahead.js] v0.10.x
* [Angular.js][angularjs]
* [jQuery][jquery] v1.9+

All of which must be loaded before *angular-typeahead.js*.

Usage
---------------

The bare bones:

```html
<script type="text/javascript" src="jquery.js"></script>
<script type="text/javascript" src="typeahead.js"></script>
<script type="text/javascript" src="bloodhound.js"></script>
<script type="text/javascript" src="angular.js"></script>
<script type="text/javascript" src="angular-typeahead.js"></script>
<script>
  // Create the application and import the siyfion.sfTypeahead dependency.
  angular.module('myApp', ['siyfion.sfTypeahead']);
</script>
<body ng-app="myApp">
    <input type="text" class="sfTypeahead" options="exampleOptions" datasets="exampleData" ng-model="foo">
    <!-- OR USING AN ATTRIBUTE -->
    <input type="text" options="exampleOptions" datasets="multiExample" ng-model="foo" sf-typeahead>
<body>
```

```javascript
// Define your own controller somewhere...
function MyCtrl($scope) {

  // Instantiate the bloodhound suggestion engine
  var numbers = new Bloodhound({
    datumTokenizer: function(d) { return Bloodhound.tokenizers.whitespace(d.num); },
    queryTokenizer: Bloodhound.tokenizers.whitespace,
    local: [
      { num: 'one' },
      { num: 'two' },
      { num: 'three' },
      { num: 'four' },
      { num: 'five' },
      { num: 'six' },
      { num: 'seven' },
      { num: 'eight' },
      { num: 'nine' },
      { num: 'ten' }
    ]
  });

  // initialize the bloodhound suggestion engine
  numbers.initialize();

  // Allows the addition of local datum
  // values to a pre-existing bloodhound engine.
  $scope.addValue = function () {
    numbers.add({
      num: 'twenty'
    });
  };

  // Typeahead options object
  $scope.exampleOptions = {
    highlight: true
  };

  // Single dataset example
  $scope.exampleData = {
    displayKey: 'num',
    source: numbers.ttAdapter()
  };

  // Multiple dataset example
  $scope.multiExample = [
    {
      name: 'nba',
      displayKey: 'team',
      source: nba.ttAdapter()   // Note the nba Bloodhound engine isn't really defined here.
    },
    {
      name: 'nhl',
      displayKey: 'team',
      source: nhl.ttAdapter()   // Note the nhl Bloodhound engine isn't really defined here.
    }
  ];

  $scope.foo = null;
};
```


<!-- assets -->
[angular-typeahead.js]: https://raw.github.com/Siyfion/angular-typeahead/master/angular-typeahead.js
[angular-typeahead.min.js]: https://raw.github.com/Siyfion/angular-typeahead/master/angular-typeahead.min.js

<!-- links to third party projects -->
[bower]: http://twitter.github.com/bower/
[jQuery]: http://jquery.com/
[angularjs]: http://angularjs.org/
[typeahead.js]: http://twitter.github.io/typeahead.js/
