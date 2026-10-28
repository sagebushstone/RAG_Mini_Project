You can programmatically add a column to a table. The PYTHON_API_TABLE table currently has two columns: TEMPERATURE and LOCATION. In this scenario, you want to add a new column named ELEVATION of type int and set it as the table's primary key.

In your next cell, run the following code:

table_details.columns.append(
 TableColumn(
   name="elevation",
   datatype="int",
   nullable=False,
   constraints=[PrimaryKey()],
 )
)

Note
This code does not create the column. Instead, this column definition is appended to the array that represents the table’s columns in the TableModel. To view this array, review the value of columns as described in the instructions for viewing the table metadata.

To modify the table and add the column, in your next cell, run the following code:
table.create_or_alter(table_details)

In this line, you call create_or_alter() on the object representing PYTHON_API_TABLE, and pass the updated value of table_details. This line adds the ELEVATION column to PYTHON_API_TABLE.

To confirm that the column was added, in your next cell, run the following code:

table.fetch().to_dict()
The output should look similar to this:

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
     {"name": "ELEVATION", "datatype": "NUMBER(38,0)", "nullable": False},
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
 "constraints": [
     {"name": "ELEVATION", "column_names": ["ELEVATION"], "constraint_type": "PRIMARY KEY"}
 ]
}
Review the value of columns and the value of constraints, both of which now include the ELEVATION column.

To confirm the existence of the new column, return to your Snowflake account in Snowsight and inspect the table.