# db-info

db-info is a utility module which provides a database independent way of
getting database metadata.

The following databases are currently supported:

 * sqlite3 - via: [node-sqlite3](https://github.com/developmentseed/node-sqlite3)
 * mysql - via: [node-mysql](https://github.com/felixge/node-mysql)

## Quick Examples
    var dbinfo = require("db-info");

    dbinfo.getInfo({
      driver: 'mysql',
      user: 'root',
      password: 'root',
      database: 'test'
    }, function(err, result) {
      /* result = {
        tables: {
          person: {
            name: 'person',
            columns: [
              { name: 'id', notNull: true, primaryKey: true, type: 'integer', length: '11' },
              { name: 'name', notNull: true, type: 'varchar', length: '255' },
              { name: 'email', notNull: false, type: 'varchar', length: '100' },
              { name: 'age', notNull: false, type: 'integer', length: '11' }
            ]
          }
        }
      } */
    });

## Download

You can install using Node Package Manager (npm):

    npm install async
    
## Documentation

### getInfo(opts, callback)

Gets the metadata from a database.

__Arguments__

 * opts - A hash of options.
  * driver - can be either "mysql" or "sqlite3"
  * _db_ - if db is passed in this connection will be used instead of making a new connection.
  * _other_ - will be passed to the drivers connect.
 * callback(err, result) - Callback called once complete. result will contain a hash containing all the tables
   along with column information.
   
__Example__
    var db = new sqlite3.Database(':memory:');
    
    dbinfo.getInfo({
      driver: 'sqlite3',
      db: db
    }, function(err, result) {
    });