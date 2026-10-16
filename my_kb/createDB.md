You can use your root object to create a database, schema, and table in your Snowflake account.

To create a database, in the next cell of your notebook, run the following code:
database = root.databases.create(
  Database(
 name="PYTHON_API_DB"),
 mode=CreateMode.or_replace
  )

This code, which is functionally equivalent to the SQL command CREATE OR REPLACE DATABASE PYTHON_API_DB, creates a database in your account named PYTHON_API_DB. This code follows a common pattern for managing objects in Snowflake:

root.databases.create() creates a database in Snowflake. It accepts two arguments: a Database object and a mode.

You pass a Database object by using Database(name="PYTHON_API_DB"), and set the name of the database by using the name argument. Recall that you imported Database on line 3 of the notebook.

You specify the creation mode by passing the mode argument. In this case, you set it to CreateMode.or_replace, but the following values are also valid:

CreateMode.if_not_exists: Functionally equivalent to CREATE IF NOT EXISTS in SQL.
CreateMode.error_if_exists: Raises an exception if the object already exists in Snowflake. This is the default value if a mode is not specified.

You manage the database programmatically by storing a reference to the database in an object you created named database.

For more information, see Managing Snowflake databases, schemas, tables, and views with Python.

Sign in to Snowsight.

In the navigation menu, select Catalog » Explorer. If your code was successful, the PYTHON_API_DB database is listed.

Tip
If you use VS Code, install the Snowflake extension to explore all Snowflake objects within your editor.

To create a schema in the PYTHON_API_DB database, in your next cell, run the following code:

schema = database.schemas.create(
  Schema(
 name="PYTHON_API_SCHEMA"),
 mode=CreateMode.or_replace,
  )
Note that you call .schemas.create() on the database object you created previously.

To create a table in the schema you just created, in your next cell, run the following code:

table = schema.tables.create(
  Table(
 name="PYTHON_API_TABLE",
 columns=[
   TableColumn(
     name="TEMPERATURE",
     datatype="int",
     nullable=False,
   ),
   TableColumn(
     name="LOCATION",
     datatype="string",
   ),
 ],
  ),
mode=CreateMode.or_replace
)
This code creates a table in the PYTHON_API_SCHEMA schema with two columns and their data types specified: TEMPERATURE as int, and LOCATION as string.

These last two code examples should look familiar because they follow the pattern in the first step where you created the PYTHON_API_DB database.

To confirm that the objects were created, return to your Snowflake account in Snowsight.