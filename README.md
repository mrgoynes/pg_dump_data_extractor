# PostgreSQL Dump CSV Extractor
This Jupyter notebook, pg_dump CSV Extractor, enables the extraction of individual PostgreSQL tables from a dump file into CSV format. This can be especially useful when working with large databases where a full restore might be prohibitive due to space limitations.

For instance, a database like USASpending, which has a full database size of over 1.5TB when including all indexes and materialized views, can be challenging to work with due to its size. This tool can extract the data from the PostgreSQL dump file and convert it into gzipped CSV files. The space required is roughly equivalent to the size of the dump file, thus considerably reducing the storage requirements.

## Features
- Extract individual PostgreSQL tables from a dump file into CSV format
- The notebook is multithreaded, allowing multiple tables to be processed concurrently for faster execution
- The size required for the extraction is about the same as the size of the dump file
- Split CSV files into manageable chunks

### Process Overview
- Set your config (db, file location, dump file location)
- Restore the schema only (no data)
- Remove constraints
- Remove indexes with dependencies
- Remove remaining indexes
- Thread the following steps for each table
  - Restore the table
  - Export the table to CSV
  - GZip (in chunks) the CSV
  - Delete the CSV
  - Truncate the table
