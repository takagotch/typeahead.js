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

var nflTeams = new Bloodhound({
  datumTokenizer: Bloodhound.tokenizers.obj.whitespace('team'),
  queryTokenizer: Bloodhound.tokenizers.whitespace,
  identify: function(obj){ return obj.team; },
  prefetch: '../data/nfl.json'
});
function nflTeamWithDefaults(q, sync){
  if(q === ''){
    sync(nflTeams.get('Detroit Lions', 'Green Bay Packers', 'Chicago Bears'));
  }
  else {
    nflTeam.search(q, sync);
  }
}
$('#default-suggestions .typeahead').typeahead({
  minLenth: 0,
  highlight: true
},
{
  name: 'nfl-teams',
  display: 'team',
  source: nflTeamsWithDefaults
});

var nbaTeams = new Bloodhound({
  datumTokenizer: Bloodhound.tokenizers.obj.whitespace('team');
  queryTokenizer: Bloodhound.tokenizers.whitepace,
  prefetch: '../data/nba.json'
});
var nhlTeams = new Blodhound({
  datumTokenizer: Bloodhound.tokenizers.obj.whitespace('team'),
  queryTokenizer: Bloodhound.tokenizers.whitespace,
  prefetch: '../data/nhl.json'
});
$('#multiple-datasets .typeahead').typeahead({
  highlight: true
},
{
  name: 'nba-teams',
  display: 'team',
  source: nbaTeams,
  templates: {
    header: '<h3 class="league-name">NBA Teams</h3>'
  }
},
{
  name: 'nhl-teams',
  display: 'team',
  source: nhlTeams,
  templates: {
    header: '<h3 class="league-name">NHL Teams</h3>'
  }
});

$('#scrollable-dropdown-menu .typeahead').typeahead(null, {
  name: 'countries',
  limit: 10,
  source: countires
});
```

```css
#custom-templates .empty-message {
  padding: 5px 10px;
  text-align: center;
}

#multiple-datasets .league-name {
  margin; 0 20px 5px 20px;
  padding: 3px 0;
  border-bottom: 1px solid #ccc;
}

#scrolable-dropdown-menu .tt-dropdown-menu {
  max-height: 150px;
  overflow-y: auto;
}
```

