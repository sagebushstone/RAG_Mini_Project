You can also manage virtual warehouses with the Snowflake Python APIs. For example, you might need to create another warehouse temporarily to run certain queries. In this scenario, you can use the API to create, suspend, or drop a warehouse.

To retrieve the collection of warehouses associated with your session, in your next cell, run the following code:
warehouses = root.warehouses
You manage warehouses in your session using the resulting warehouses object.

To define and create a new warehouse, in your next cell, run the following code:
python_api_wh = Warehouse(
 name="PYTHON_API_WH",
 warehouse_size="SMALL",
 auto_suspend=500,
)

warehouse = warehouses.create(python_api_wh,mode=CreateMode.or_replace)
In this code, you define a new warehouse by instantiating Warehouse and specifying the warehouse’s name, size, and auto-suspend policy. The auto-suspend timeout is in units of seconds. In this case, the warehouse will be suspended after 8.33 minutes of inactivity.

You then create the warehouse by calling create() on your warehouse collection. You store the reference in the resulting warehouse object.

Navigate to your Snowflake account in Snowsight and confirm that the warehouse was created.

To retrieve information about the warehouse, in your next cell, run the following code:
warehouse_details = warehouse.fetch()
warehouse_details.to_dict()
This code should look familiar because it follows the same pattern you used to fetch table metadata in a previous step. The output should be similar to this:
{
  'name': 'PYTHON_API_WH',
  'auto_suspend': 500,
  'auto_resume': 'true',
  'resource_monitor': 'null',
  'comment': '',
  'max_concurrency_level': 8,
  'statement_queued_timeout_in_seconds': 0,
  'statement_timeout_in_seconds': 172800,
  'tags': {},
  'warehouse_type': 'STANDARD',
  'warehouse_size': 'Small'
}
Optional: If you have multiple warehouses in your session, use the API to iterate through them or to search for a specific warehouse.

In your next cell, run the following code:
warehouse_list = warehouses.iter(like="PYTHON_API_WH")
result = next(warehouse_list)
result.to_dict()

In this code, you call iter() on the warehouse collection and pass the like argument, which returns any warehouses whose names match the specified string. In this case, you pass the name of the warehouse you defined previously, but this argument is generally a case-insensitive string that functions as a filter, with support for SQL wildcard characters like % and _.

After you run the cell, output similar to the following code shows that you successfully returned a matching warehouse:
{
  'name': 'PYTHON_API_WH',
  'auto_suspend': 500,
  'auto_resume': 'true',
  'resource_monitor': 'null',
  'comment': '',
  'max_concurrency_level': 8,
  'statement_queued_timeout_in_seconds': 0,
  'statement_timeout_in_seconds': 172800,
  'tags': {},
  'warehouse_type': 'STANDARD',
  'warehouse_size': 'Small'
}

To programmatically modify the warehouse by changing its size to LARGE, in your next cell, run the following code:
warehouse = root.warehouses.create(Warehouse(
 name="PYTHON_API_WH",
 warehouse_size="LARGE",
 auto_suspend=500,
), mode=CreateMode.or_replace)
To confirm that the warehouse size was updated to LARGE, do one of the following:

In your next cell, run the following code:
warehouse.fetch().size

Navigate to your Snowflake account in Snowsight and confirm the change in warehouse size.

Optional: If you don’t want to continue using the warehouse, drop it. In your next cell, run the following code:
warehouse.drop()

To confirm the warehouse deletion, return to your Snowflake account in Snowsight.