## Snapshots

Snapshots are crunch entities such as analyses that can be shared externally to crunch, such as an embed link.

### Catalog

`/snapshots/`

#### GET

```http
GET /snapshots/ HTTP/1.1
Host: beta.crunch.io
--------
200 OK
Content-Type: application/json
```

```
// Example snapshot catalog:
```

```json
{
    "self": "http://local.crunch.io:5051/api/snapshots/", 
    "description": "List the available snapshots of visible for this user", 
    "element": "shoji:catalog",
    "index": {
        "http://crunch.io/api/snapshots/f320a58264984021b2cf5230d316e49f/": {
            "url": "http://crunch.io/cdn/snapshots/f320a58264984021b2cf5230d316e49f.json", 
            "timestamp": "2015-11-04T21:36:33.897000+00:00", 
            "reference": "http://local.crunch.io:5051/api/datasets/ds_id/decks/deck_id/"
        }
    } 
}
```

#### POST

To create a new snapshot, POST a Shoji Entity with a snapshot a list of queries in the body.
The queries are cube expressions that define the analysis requested.
The currently applied filters and weights will utilized when computing the result.  

```http
POST /snapshots/ HTTP/1.1
Host: beta.crunch.io
Content-Type: application/json
...
{"body": {"queries": [{"dimensions": [{"args": [{"variable": "http://crunch.io/api/datasets/c9fb9d6cba9a4617bf14ae5e8a12f602/variables/000000/"}],
                                       "function": "bin"}],
                       "measures": {"count": {"function": "cube_count"}}}],
          "reference": "/datasets/ds_id/decks/deck_id/"},
 "element": "shoji:entity"}
--------
201 Created
Location: /snapshots/03df2a/
```
