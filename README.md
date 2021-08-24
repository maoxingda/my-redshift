# Amazon Redshift

## SQL reference

### SQL commands

##### COPY

Loads data into a table from:

- data files can be located in:
  - Amazon EMR cluster
  - Amazon Simple Storage Service (Amazon S3) bucket
  - remote host that is accessed using a Secure Shell (SSH) connection
- Amazon DynamoDB table

:warning:

- Amazon Redshift Spectrum external tables are read-only. You can't COPY to an external table.
- The COPY command appends the new input data to any existing rows in the table.
- The maximum size of a single input row from any source is 4 MB.
- The table can be temporary or persistent. 

###### COPY syntax

```sql
COPY table-name 
[ column-list ]
FROM data_source
authorization
[ [ FORMAT ] [ AS ] data_format ] 
[ parameter [ argument ] [, ... ] ]
```

###### Data format parameters

You can load data from text files in fixed-width, character-delimited, comma-separated values (CSV), or JSON format, or from Avro files.

By default, the COPY command expects the source data to be in character-delimited UTF-8 text files. The default delimiter is a pipe character ( | ). If the source data is in another format, use the following parameters to specify the data format.

- [FORMAT](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-format.html#copy-format)
- [CSV](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-format.html#copy-csv)
- [DELIMITER](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-format.html#copy-delimiter)
- [FIXEDWIDTH](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-format.html#copy-fixedwidth)
- [SHAPEFILE](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-format.html#copy-shapefile)
- [AVRO](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-format.html#copy-avro)
- [JSON](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-format.html#copy-json)
- [ENCRYPTED](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-source-s3.html#copy-encrypted)
- [BZIP2](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-file-compression.html#copy-bzip2)
- [GZIP](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-file-compression.html#copy-gzip)
- [LZOP](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-file-compression.html#copy-lzop)
- [PARQUET](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-format.html#copy-parquet)
- [ORC](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-format.html#copy-orc)
- [ZSTD](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-file-compression.html#copy-zstd)

As it loads the table, COPY attempts to implicitly convert the strings in the source data to the data type of the target column. If you need to specify a conversion that is different from the default behavior, or if the default conversion results in errors, you can manage data conversions by specifying the following parameters.

- [ACCEPTANYDATE](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-acceptanydate)
- [ACCEPTINVCHARS](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-acceptinvchars)
- [BLANKSASNULL](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-blanksasnull)
- [DATEFORMAT](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-dateformat)
- [EMPTYASNULL](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-emptyasnull)
- [ENCODING](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-encoding)
- [ESCAPE](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-escape)
- [EXPLICIT_IDS](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-explicit-ids)
- [FILLRECORD](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-fillrecord)
- [IGNOREBLANKLINES](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-ignoreblanklines)
- [IGNOREHEADER](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-ignoreheader)
- [NULL AS](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-null-as)
- [REMOVEQUOTES](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-removequotes)
- [ROUNDEC](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-roundec)
- [TIMEFORMAT](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-timeformat)
- [TRIMBLANKS](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-trimblanks)
- [TRUNCATECOLUMNS](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-conversion.html#copy-truncatecolumns)

###### Data load operations

Manage the default behavior of the load operation for troubleshooting or to reduce load times by specifying the following parameters.

- [NOLOAD](https://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-data-load.html#copy-noload)

###### Using the COPY command

For more information about how to use the COPY command, see the following topics:

- [COPY examples](https://docs.aws.amazon.com/redshift/latest/dg/r_COPY_command_examples.html)
- [Usage notes](https://docs.aws.amazon.com/redshift/latest/dg/r_COPY_usage_notes.html)
- [Tutorial: Loading data from Amazon S3](https://docs.aws.amazon.com/redshift/latest/dg/tutorial-loading-data.html)
- [Amazon Redshift best practices for loading data](https://docs.aws.amazon.com/redshift/latest/dg/c_loading-data-best-practices.html)
- [Using a COPY command to load data](https://docs.aws.amazon.com/redshift/latest/dg/t_Loading_tables_with_the_COPY_command.html)
  - [Loading data from Amazon S3](https://docs.aws.amazon.com/redshift/latest/dg/t_Loading-data-from-S3.html)
  - [Loading data from Amazon EMR](https://docs.aws.amazon.com/redshift/latest/dg/loading-data-from-emr.html)
  - [Loading data from remote hosts](https://docs.aws.amazon.com/redshift/latest/dg/loading-data-from-remote-hosts.html)
  - [Loading data from an Amazon DynamoDB table](https://docs.aws.amazon.com/redshift/latest/dg/t_Loading-data-from-dynamodb.html)
- [Troubleshooting data loads](https://docs.aws.amazon.com/redshift/latest/dg/t_Troubleshooting_load_errors.html)

###### COPY parameter reference

