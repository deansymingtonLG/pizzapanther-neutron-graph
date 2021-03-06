# Neutron-Graph
A small GraphQL Query generator

## Requirements

- Promise based HTTP client (Default: Axios or $http for Angular)
- ES6 style Promises (Default: Promise or $q for Angular)

## Browser Based Usage

Include Script: `browser-dist/neutron-graph.js `

Usage:

```javascript
var neutron_graph = require('neutron-graph');
GraphAPI = neutron_graph.default('/graphql', {http: $http, promise: $q});

var query = {
  node: 'allSchedules',
  filters: {user_RemoteUserId: 5},
  attributes: ['id', 'sunday', 'monday',]
};

GraphAPI().data_graph().all(query).submit().then(function(response) {
  console.log(response.data.allSchedules.nodes());
}).catch(function(error) {
  console.log(error);
});
```

## ES6 Usage

```javascript
import DataGraph from './node_modules/neutron-graph/neutron-graph';

var verses;
var GraphAPI = DataGraph('/data-graph');

var query = {
  node: 'allVerses',
  filters: {book_Slug: 'my-book', chapter: 2},
  attributes: ['text', 'verse']
};

GraphAPI().all(query).submit().then(function (result) {
  verses = result.data.allVerses.nodes();
}).catch(function (error) {
  console.error(error);
});
```

## API

### Chaining

```javascript
var GraphAPI = DataGraph('/data-graph');
var promise = GraphAPI().all(query1).all(query2).get(query3).submit();
```

Result will contain an attribute for each node name.

Example: `result.data.AllVerses, result.data.AllChapters, result.data.Chapter`

### Query Methods

|Name|Description|
|------|-----------|
|all()|Query that contains multiple results|
|get()|Query by ID. Supply base64 `{id}` or `{name, id}` to generate id|


### QueryResult Attributes

|Name|Description|
|------|-----------|
|data|DataTransformer objects named by node names|
|query|original text query generated|
|response|original response object|


### DataTransformer Methods and Attributes

|Name|Description|
|------|-----------|
|data|original data|
|nodes()|list data extracted from edges list and node object|
|first()|get first node and return it|
|last()|get last node and return it|
# pizzapanther-neutron-graph
