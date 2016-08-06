Using UltraForms
================

Ultraforms is a dynamic forms system built on angular.  It uses UltraDb for persistence.

It can create a completely functional form which can load and save data in as little as 3 lines of html.  No other code is required.

# Creating a form for an entity

In your html file, before the closing </body> tag, include the following lines...

    <script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.4.5/angular.js"></script>

    <script src="js/dynamicForms/DynamicForms.js"></script>

    <script src="js/dynamicForms/DynamicDataFactory.js"></script>

    <script src="js/dynamicForms/EntityServices.js"></script>
    <script src="js/dynamicForms/FormMetaDataService.js"></script>

    <script src="js/dynamicForms/DynamicEntityDirective.js"></script>

    <script src="js/dynamicForms/DynamicFormDirective.js"></script>
    <script src="js/dynamicForms/DynamicTableDirective.js"></script>


     <title>TODO supply a title</title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
    </head>
    <body>
        <div>Customizing Dynamic Forms (without having to write any code)</div>
        <article>
            The EntityDataSource class that you provide contains a method named getMetaSchema() that returns the name of the
            schema in your database where it should look for a table named FormMetaData.
            
            By inserting rows in this table, you can customize the handling of any table column in any or all views, as desired.
            
            When an entity is loaded, all of the relevant form meta data is extracted from the ResultSet and is then stored in the Entity instance.
            if caching is on, which it is by default, all instances of an entity which have the same name (or view name if a view), will
            share the first instance of the form meta data that gets created using that name.  
            
            UltraForms is designed to allow you to customize the content of that meta data for all instances of a given field, or for a given field
            in any specific views you desire.  This customization is performed by adding records to the formMetaData table, and in most instances,
            no coding will be required.  
            
            After extracting the dynamic meta data associated with an entity, the contents of the formMetaData table are applied using a simple set of rules.
            
            Any records which are found to apply to the entity in the desired view are applied over the existing dynamic data.  This allows 
            you to override default values, as well as add new values which you can use for whatever purpose you like.
            
            1) schematable and viewname are the same - These are default overrides which will be applied to all instances of the 
            entity.  
            2) schematable and viewname are different - applied only for the specifically named view.
            
            Because of the order in which they are applied, you are able to effect all or specific entities as needed.
            
            This mechanism allows you to do many things easily when using UltraForms.  The most widely desired things you might want to do are...

            * Change the component type for a field globally or only in specific views.
            * Inject customized HTML including angular directly into dynamically generated forms - globally or only in specific views.
            * Add new fields to an entity or view that don't actually exist in the database table.
            
            
            Change the component type associated with a given table column - i.e. from a simple text edit to perhaps a masked edit or even a combo box or checkbox.
            And because the mechanism lets you specify views, you can have different information for the same field - ie. a given table field may be 
            a text edit in one view and a checkbox in another.
            
            CUSTOMIZING a dynamic UltraForm!
            This is where things get very interesting, and this is where other libraries would probably become very complex.  Not so here!
            You can cause any custom HTML, including angular directives or whatever, for any given field, by simply adding a row to the formmetadata
            table for the desired table, column and view, and set the label to "html".  The value for the html label is a URL, from which it 
            will load your html.  Ultraforms will sanitize and compile whatever it loads, and insert it into the dynamically generated form or table
            when the specified column is being rendered.
            This should make just about any customizations possible, and if applied at the table level (ie, table name and view name the same), then 
            your customizations will be applied everywhere the field appears, unless it is overridden in a particular view.  In other words, you won't need
            to do anything going forward to have your customization applied, even in new views.
            
            Other labels
            
            ComboBoxes
            
            If you change the "type" label of a given field to "combobox", then you must also add the valueList label as well, and set its value to the name of the value list to use for 
            the combobox.  No additional code is needed - the field will appear on the desired ultraforms or tables as a combobox with the value list set as the available options.
            
            
            
            
        </article>
    </body>
</html>
