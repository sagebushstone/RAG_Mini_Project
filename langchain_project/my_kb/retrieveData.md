You can retrieve metadata about an object in Snowflake.

To retrieve details about the PYTHON_API_TABLE table you created previously, in your next notebook cell, run the following code:

table_details = table.fetch()
fetch() returns a TableModel object.

You can then call .to_dict() on the resulting object to view its detailed information.

To print the table details, in your next cell, run the following code:

table_details.to_dict()
The notebook should display a dictionary that contains metadata about the PYTHON_API_TABLE table, similar to this:

{
 "name": "PYTHON_API_TABLE",
 "kind": "TABLE",
 "enable_schema_evolution": False,
 "change_tracking": False,
 "data_retention_time_in_days": 1,
 "max_data_extension_time_in_days": 14,
 "default_ddl_collation": "",
 "columns": [
     {"name": "TEMPERATURE", "datatype": "NUMBER(38,0)", "nullable": False},
     {"name": "LOCATION", "datatype": "VARCHAR(16777216)", "nullable": True},
 ],
 "created_on": datetime.datetime(
     2024, 5, 9, 8, 59, 15, 832000, tzinfo=datetime.timezone.utc
 ),
 "database_name": "PYTHON_API_DB",
 "schema_name": "PYTHON_API_SCHEMA",
 "rows": 0,
 "bytes": 0,
 "owner": "ACCOUNTADMIN",
 "automatic_clustering": False,
 "search_optimization": False,
 "owner_role_type": "ROLE",
}
As shown, this dictionary contains information about the PYTHON_API_TABLE table that you created previously, with detailed information about columns, owner, database, schema, and more.

Object metadata is useful when you are building business logic in your application. For example, you might build logic that runs depending on certain information about an object. You can use fetch() to retrieve object metadata in such scenarios.