# Migrations

sqlc will ignore rollback statements when parsing migration SQL files. The following tools are current supported:

- [goose](https://github.com/pressly/goose)
- [sql-migrate](https://github.com/rubenv/sql-migrate)

## goose

```sql
-- +goose Up
CREATE TABLE post (
    id    int NOT NULL,
    title text,
    body  text,
    PRIMARY KEY(id)
);

-- +goose Down
DROP TABLE post;
```

```go
package db

type Post struct {
	ID    int
	Title sql.NullString
	Body  sql.NullString
}
```

### sql-migrate

```sql
-- +migrate Up
-- SQL in section 'Up' is executed when this migration is applied
CREATE TABLE people (id int);


-- +migrate Down
-- SQL section 'Down' is executed when this migration is rolled back
DROP TABLE people;
```

```go
package db

type People struct {
	ID    int32
}
```
