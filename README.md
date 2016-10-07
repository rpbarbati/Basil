# Basil
Basil is angular dynamic forms and tables for Tomato Entities.

Tomato is a light-weight Java based ORM persistence layer with zero dependencies.  
It is everything you want for data access, without all the configuration and code that Spring Data requires.

Basil is dependent on Tomato, so you must download both projects.  
The POM files are configured so that Tomato is a Java project and Basil is a web project which has a dependency to the Tomato project.
Basil contains several servlets which provide the support for angular to read and write Tomato data and form schema information.

After downloading and configuring both projects, you can verify your installation by opening the EntityTester/EntityTester.html 
file in your browser.
The page has several fields and a text area.  
Type the schema.tableName into the schema.tableName field (the first field)
click the New Button.
The text window should be populated with the entity definition for the entered schema.tableName.
To load a specific row, provide the key values in the entity definition.
To load a set of rows, set the __filter to a valid condition ("1=1" will load all rows).
Click the Load button to execute the query that is in the text window.

If you download both Tomato and Basil, here are some of the things you can do...

#What are the directives...
dynamic-entity loads an entity based on the JSON its key is set to.
dynamic-collection loads an entity set based on the name and filter values provided.
Both dynamic-entity and dynamic-collection act as hosts for the loaded data.
You will use either dynamic-form and dynamic-table to display that hosted data.

# An HTML table with the ability to Add, Edit and Delete rows from any table in any schema
- just replace schema.tableName below with the desired schema.tableName.

```
<dynamic-collection name="schema.tableName" filter="1=1">

      <dynamic-table name="schema.tableName" path="schema.tableName" add="addRow" update="updateRow" delete="deleteRow">
        <!-- add, update and delete are given methods that reside in the dynamic-collection controller -->
        <!-- If you don't want to enable a feature, like add, then do not set its attribute.  If not set, no button will appear to invoke it -->

      </dynamic-table>

    </dynamic-collection>
```

# A dynamic form for any schema.tableName
- replace schema.tableName below with the desired schema.tableName.
- replace key_field_name with the name of a key field
- replace key with a valid key value
```
    <dynamic-entity name="schema.tableName" key="{"key_field_name": key}">

      <dynamic-form name="schema.tableName" path="schema.tableName">
      </dynamic-form>

    </dynamic-entity>
```

# A dynamic form and a table for a hierarchical data set
In this example, I am loading a view which consists of an order entity with an embedded set of line items.
- replace schema.tableName below with the desired schema.tableName.
- replace key_field_name with the name of a key field
- replace key with a valid key value
```
    <dynamic-entity name="schema.orders" deep="true" key="{'order_id': 1}">
    <!-- set deep to true to load child entities -->

      <!-- Present the detail form for the order -->
      <dynamic-form name="schema.orders" path="schema.orders">
      </dynamic-form>

      <!-- Create the table to display the embedded line items -->
      <dynamic-table  name="schema.lineItems" path="schema.orders.schema.lineItems">
        <!-- Notice the path leads to the embedded collection of line items, which is a child of Orders -->

      </dynamic-table>

    </dynamic-entity>
```


