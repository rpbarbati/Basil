Using Basil
================

# Creating forms and tables for entities and entity collections

In your html file, before the closing </body> tag, include the following lines...

    <script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.4.5/angular.js"></script>

    <script src="js/dynamicForms/DynamicForms.js"></script>

    <script src="js/dynamicForms/DynamicDataFactory.js"></script>

    <script src="js/dynamicForms/EntityServices.js"></script>
    <script src="js/dynamicForms/FormMetaDataService.js"></script>

    <script src="js/dynamicForms/DynamicEntityDirective.js"></script>

    <script src="js/dynamicForms/DynamicFormDirective.js"></script>
    <script src="js/dynamicForms/DynamicTableDirective.js"></script>

# To create a form for a table in your database

Paste the following lines into the body of your page.

    <dynamic-entity name="sakila.staff" deep="false" keys="{'staff_id': 1}">

        <dynamic-form name="sakila.staff" path="sakila.staff"></dynamic-form>

    </dynamic-entity>

The dynamic-entity element is used to load data for simple testing.  It acts as a host for an entity.  
Use the keys attribute to specify a key value which specifies the record to load.
The dynamic-form element renders a form for the data loaded by the dynamic-entity element.
For data hierarchies, the path should specify the path to the desired entity.  For example, to render a form for 
a child record of staff, for example, from the rental table, the path would be "sakila.staff.sakila.rental".  
All entities always use schema.tableOrViewName, whether nested or not.

# To create a table for a collection of rows

    <dynamic-collection name="sakila.staff" filter="1=1">

        <dynamic-table name="sakila.staff" path="sakila.staff"></dynamic-table>

    </dynamic-collection>

The dynamic-collection element loads all records from the sakila.staff table.
The dynamic-table element renders the rows loaded by the dynamic-collection element. 
The rendered table supports adding, updating, and deleting rows.  You can use these options by passing a method to any of the following attributes on the dynamic-table element.

    add=
    update=
    delete=



        <div>Customizing Dynamic Forms (without having to write any code)</div>
        <article>
            The EntityDataSource class that you provide contains a method named getMetaSchema() that returns the name of the
            schema in your database where it should look for a table named FormMetaData.
            
            By inserting rows in this table, you can customize the handling of any table column in any or all views, as desired.
            
            When an entity is loaded, all of the relevant form meta data is extracted from the ResultSet and is then stored in the Entity instance.
            if caching is on, which it is by default, all instances of an entity which have the same name (or view name if a view), will
            share the first instance of the form meta data that gets created using that name.  
            
            Basil is designed to allow you to customize the content of that meta data for all instances of a given field, or for a given field
            in any specific views you desire.  This customization is performed by adding records to the formMetaData table, and in most instances,
            no coding will be required.  
            
            After extracting the dynamic meta data associated with an entity, the contents of the formMetaData table are applied using a simple set of rules.
            
            Any records which are found to apply to the entity in the desired view are applied over the existing dynamic data.  This allows 
            you to override default values, as well as add new values which you can use for whatever purpose you like.  These are the rules that Tomato applies to rows in FormMetaData.
            
            1) If schematable and viewname are the same - These are default overrides which will be applied to all instances of the entity.  
            2) If schematable and viewname are different - applied only for the specifically named view.
            
            Because of the order in which they are applied, you are able to effect all or specific entities as needed.
            
            This mechanism allows you to do many things easily when using Basil.  The most widely desired things you might want to do are...

            1) Change the component type for a field globally or only in specific views.
            2) Inject customized HTML for a column or other purpose directly into dynamically generated forms and tables - globally or only in specific views.
            3) Add new fields to an entity or view that don't actually exist in the database table.
            
            
            1) Change the component type associated with a given table column - i.e. from a simple text edit to perhaps a masked edit or even a combo box or checkbox.
            And because the mechanism lets you specify views, you can have different information for the same field - ie. a given table field may be 
            a text edit in one view and a checkbox in another.
            
            2) CUSTOMIZING a dynamic Basil form!
            You can cause any custom HTML, including angular directives or whatever, for any given field, by simply adding a row to the formmetadata
            table for the desired table, column and view, and set the label to "html".  The value for the html label is a URL, from which it 
            will load your html.  Basil will sanitize and compile whatever it loads, and insert it into the dynamically generated form or table
            when the specified column is being rendered.
            This should make just about any customizations possible, and if applied at the table level (ie, table name and view name the same), then 
            your customizations will be applied everywhere the field appears, unless it is overridden in a particular view.  In other words, you won't need
            to do anything going forward to have your customization applied, even in new views.
            
            Other labels
            
            ComboBoxes
            
            If you change the "type" label of a given field to "combobox", then you must also add the valueList label as well, and set its value to the name of the value list to use for 
            the combobox.  No additional code is needed - the field will appear on the desired basil forms or tables as a combobox with the value list set as the available options.
            
            
            
            
        </article>
    </body>
</html>
