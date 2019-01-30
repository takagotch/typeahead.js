### typeahead.js
---
https://github.com/twitter/typeahead.js

```js
var substringMatcher = function(strs){
  return function findMatches(q, cb){
    var matches, substringRegex;
    matches = [];
    substrRegex = new RegExp(q, 'i');
    $.each(strs, function(i, str){
      if(substrRegex.test(str)){
        matches.push(str);
      }
    });
    cb(matches);
  };
};
var states = ['', '', '', '', '',
  '', '', '', '', '', '', '', ''];
$('#the-basic .typeahead').typeahead({
  hint: true,
  highlight: true,
  minlength: 1
},
{
  name: 'states',
  source: substringMatcher(states)
});  
```

```js
var states = new Bloodhound({

});
$('#bloodhound .typeahead').typeahead({
  hint: true,
  highlight: true,
  minLength: 1
},
{
  name: 'states',
  source: states
});

var countries = new Bloodhound({
  datumTokenizer: Bloodhound.tokenizers.whitespace,
  queryTokenizer: Bloodhound.tokenizers.whitespace,
  prefetch: '../data/countries.json'
});
$('#prefetch .typeahead').typeahead(null, {
  name: 'countries',
  source: countries
});

var bestPictures = new Bloodhound({
  datumTokenizer: Bloodhound.tokenizers.obj.whitespace('value'),
  queryTokenizer: Bloodhound.tokenizers.whitespace,
  prefetch: '../data/films/post_1960.json',
  remote: {
    url: '../data/films/queries/%QUERY.json',
    wildcard: '%QUERY'
  }
});
$('#remote .typeahead').typeahead(null, {
  name: 'best-pictures',
  display: 'value',
  source: bestPictures
});

$('#custom-tempaltes .typeahead').typeahead(null, {
  name: 'best-pictures',
  display: 'value',
  source: bestPictures,
  templates: {
    empty: [
      '<div class="empty-message">',
        'unable to find any Best Picture winners that match the current query',
      '</div>'
    ].join('\n'),
    suggestion: Handlebars.compile('<div><strong>{{value}}</strong> - {{year}}</div>')
  }
});
```

```css
#custom-templates .empty-message {
  padding: 5px 10px;
  text-align: center;
}
```

