Class **Phalcon\\Mvc\\Model\\Query**
====================================

*implements* :doc:`Phalcon\\Mvc\\Model\\QueryInterface <Phalcon_Mvc_Model_QueryInterface>`, :doc:`Phalcon\\Di\\InjectionAwareInterface <Phalcon_Di_InjectionAwareInterface>`

This class takes a PHQL intermediate representation and executes it.  

.. code-block:: php

    <?php

     $phql = "SELECT c.price*0.16 AS taxes, c.* FROM Cars AS c JOIN Brands AS b
              WHERE b.name = :name: ORDER BY c.name";
    
     $result = manager->executeQuery($phql, array(
       "name": "Lamborghini"
     ));
    
     foreach ($result as $row) {
       echo "Name: ",  $row->cars->name, "\n";
       echo "Price: ", $row->cars->price, "\n";
       echo "Taxes: ", $row->taxes, "\n";
     }



Constants
---------

*integer* **TYPE_SELECT**

*integer* **TYPE_INSERT**

*integer* **TYPE_UPDATE**

*integer* **TYPE_DELETE**

Methods
-------

public  **__construct** ([*unknown* $phql], [*unknown* $dependencyInjector])

Phalcon\\Mvc\\Model\\Query constructor



public  **setDI** (*unknown* $dependencyInjector)

Sets the dependency injection container



public  **getDI** ()

Returns the dependency injection container



public  **setUniqueRow** (*unknown* $uniqueRow)

Tells to the query if only the first row in the resultset must be returned



public  **getUniqueRow** ()

Check if the query is programmed to get only the first row in the resultset



final protected  **_getQualified** (*unknown* $expr)

Replaces the model's name to its source name in a qualifed-name expression



final protected  **_getCallArgument** (*unknown* $argument)

Resolves a expression in a single call argument



final protected  **_getCaseExpression** (*unknown* $expr)

Resolves a expression in a single call argument



final protected  **_getFunctionCall** (*unknown* $expr)

Resolves a expression in a single call argument



final protected *string*  **_getExpression** (*unknown* $expr, [*unknown* $quoting])

Resolves an expression from its intermediate code into a string



final protected *array*  **_getSelectColumn** (*unknown* $column)

Resolves a column from its intermediate representation into an array used to determine if the resultset produced is simple or complex



final protected *string*  **_getTable** (*unknown* $manager, *unknown* $qualifiedName)

Resolves a table in a SELECT statement checking if the model exists



final protected *array*  **_getJoin** (*unknown* $manager, *unknown* $join)

Resolves a JOIN clause checking if the associated models exist



final protected *string*  **_getJoinType** (*unknown* $join)

Resolves a JOIN type



final protected *array*  **_getSingleJoin** (*unknown* $joinType, *unknown* $joinSource, *unknown* $modelAlias, *unknown* $joinAlias, *unknown* $relation)

Resolves joins involving has-one/belongs-to/has-many relations



final protected *array*  **_getMultiJoin** (*unknown* $joinType, *unknown* $joinSource, *unknown* $modelAlias, *unknown* $joinAlias, *unknown* $relation)

Resolves joins involving many-to-many relations



final protected *array*  **_getJoins** (*unknown* $select)

Processes the JOINs in the query returning an internal representation for the database dialect



final protected *array*  **_getOrderClause** (*array|string* $order)

Returns a processed order clause for a SELECT statement



final protected  **_getGroupClause** (*unknown* $group)

Returns a processed group clause for a SELECT statement



final protected  **_getLimitClause** (*unknown* $limitClause)

Returns a processed limit clause for a SELECT statement



final protected  **_prepareSelect** ([*unknown* $ast], [*unknown* $merge])

Analyzes a SELECT intermediate code and produces an array to be executed later



final protected  **_prepareInsert** ()

Analyzes an INSERT intermediate code and produces an array to be executed later



final protected  **_prepareUpdate** ()

Analyzes an UPDATE intermediate code and produces an array to be executed later



final protected  **_prepareDelete** ()

Analyzes a DELETE intermediate code and produces an array to be executed later



public  **parse** ()

Parses the intermediate code produced by Phalcon\\Mvc\\Model\\Query\\Lang generating another intermediate representation that could be executed by Phalcon\\Mvc\\Model\\Query



public  **getCache** ()

Returns the current cache backend instance



final protected  **_executeSelect** (*unknown* $intermediate, *unknown* $bindParams, *unknown* $bindTypes, [*unknown* $simulate])

Executes the SELECT intermediate representation producing a Phalcon\\Mvc\\Model\\Resultset



final protected :doc:`Phalcon\\Mvc\\Model\\Query\\StatusInterface <Phalcon_Mvc_Model_Query_StatusInterface>`  **_executeInsert** (*unknown* $intermediate, *unknown* $bindParams, *unknown* $bindTypes)

Executes the INSERT intermediate representation producing a Phalcon\\Mvc\\Model\\Query\\Status



final protected :doc:`Phalcon\\Mvc\\Model\\Query\\StatusInterface <Phalcon_Mvc_Model_Query_StatusInterface>`  **_executeUpdate** (*unknown* $intermediate, *unknown* $bindParams, *unknown* $bindTypes)

Executes the UPDATE intermediate representation producing a Phalcon\\Mvc\\Model\\Query\\Status



final protected :doc:`Phalcon\\Mvc\\Model\\Query\\StatusInterface <Phalcon_Mvc_Model_Query_StatusInterface>`  **_executeDelete** (*unknown* $intermediate, *unknown* $bindParams, *unknown* $bindTypes)

Executes the DELETE intermediate representation producing a Phalcon\\Mvc\\Model\\Query\\Status



final protected :doc:`Phalcon\\Mvc\\Model\\ResultsetInterface <Phalcon_Mvc_Model_ResultsetInterface>`  **_getRelatedRecords** (*unknown* $model, *unknown* $intermediate, *unknown* $bindParams, *unknown* $bindTypes)

Query the records on which the UPDATE/DELETE operation well be done



public *mixed*  **execute** ([*unknown* $bindParams], [*unknown* $bindTypes])

Executes a parsed PHQL statement



public *Ṕhalcon\Mvc\ModelInterface*  **getSingleResult** ([*unknown* $bindParams], [*unknown* $bindTypes])

Executes the query returning the first result



public  **setType** (*unknown* $type)

Sets the type of PHQL statement to be executed



public  **getType** ()

Gets the type of PHQL statement executed



public  **setBindParams** (*unknown* $bindParams, [*unknown* $merge])

Set default bind parameters



public *array*  **getBindParams** ()

Returns default bind params



public  **setBindTypes** (*unknown* $bindTypes, [*unknown* $merge])

Set default bind parameters



public *array*  **getBindTypes** ()

Returns default bind types



public  **setIntermediate** (*unknown* $intermediate)

Allows to set the IR to be executed



public *array*  **getIntermediate** ()

Returns the intermediate representation of the PHQL statement



public  **cache** (*unknown* $cacheOptions)

Sets the cache parameters of the query



public  **getCacheOptions** ()

Returns the current cache options



public  **getSql** ()

Returns the SQL to be generated by the internal PHQL (only works in SELECT statements)



