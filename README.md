
# node-mysql-paginate


> `node-mysql-paginate` is a library for [node-mysql][node-mysql] to easily add paginated queries and results. This lib was inspired in work of [mongoose-paginate][mongoose-paginate] library.  


## Index

* [Install](#install)
* [Usage](#usage)
* [Contributors](#contributors)
* [License](#license)


## Install

```bash
npm install -S niltonvasques/node-mysql-paginate
```


## Usage

```js

var paginate = require('node-mysql-paginate');

```

### paginate.paginate(connection, query, options, callback)

**Arguments**

* `connectiony` - node-mysql connection object.
* `query` - MySQL String query.
* `options` - paginated options  
  - `page` - Default: `1`
  - `limit` - Default: `10`
  - `columns` - Default: `null`
  - `params` - Default: `null` - Arguments to be passed to SQL Query. 
* `callback(err, results)` - A callback which is called once pagination results are retrieved, or when an error has occurred.

**Examples**

```js
var paginate    = require('node-mysql-paginate');

function paginated_query(req, res, query, params){
  var limit = 10;
  if(req.query.limit){
    limit = req.query.limit;
  }
  var page = 1;
  if(req.query.page){
    page = req.query.page;
  }
  paginate.paginate(database.connection, query, 
      {
        page : page,
        limit: limit,
        params: params 
      },
      function (err, rows){
        if(err){
          console.log("An unexpected error happens.");
          return;
        }
        res.json(rows);
      }
  );
}
```

## Contributors

* Nilton Vasques <nilton.vasques@gmail.com>

## License

[MIT][license-url]

[license-url]: LICENSE
[node-mysql]: https://github.com/felixge/node-mysql 
[mongoose-paginate]: http://github.com/edwardhotchkiss/mongoose-paginate
