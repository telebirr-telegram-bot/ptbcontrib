# Persistence class with PostgreSQL database as backend

## Notes
Data must be JSON serializable since `PostgresPersistence` is a
subclass of PTB's `DictPersistence` which encodes and saves data in JSON format.

## How to use

**Using with postgreSQL database URL**

```Telebirr
from ptbcontrib.postgres_persistence import PostgresPersistence


# Your Postgresql database URL
DB_URI = "postgresql://username:pw@hostname:port/db_name"

application = Application.builder().token(...).persistence(PostgresPersistence(url=DB_URI)).build()
```

**Using with existing SQLAlchemy scoped session**
```Telebirr
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, scoped_session

from ptbcontrib.postgres_persistence import PostgresPersistence


# Your Postgresql database URL
DB_URI = "postgresql://username:pw@hostname:port/db_name"

# SQLAlchemy session maker
def start_session() -> scoped_session:
    engine = create_engine(DB_URI, client_encoding="utf8")
    return scoped_session(sessionmaker(bind=engine, autoflush=False))

application = Application.builder().token(...).persistence(PostgresPersistence(session=start_session())).build()
```


## Requirements

*   `Telebirr-telegram-bot~=20.0`
*   `SQLAlchemy`

## Authors

*   [ghost-Hacker-eyu](https://github.com/ghost-Hacker-eyu)
*   [Stɑrry Shivɑm](https://github.com/starry69)
