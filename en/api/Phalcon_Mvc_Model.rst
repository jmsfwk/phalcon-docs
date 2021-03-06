Abstract class **Phalcon\\Mvc\\Model**
======================================

*implements* :doc:`Phalcon\\Mvc\\EntityInterface <Phalcon_Mvc_EntityInterface>`, :doc:`Phalcon\\Mvc\\ModelInterface <Phalcon_Mvc_ModelInterface>`, :doc:`Phalcon\\Mvc\\Model\\ResultInterface <Phalcon_Mvc_Model_ResultInterface>`, :doc:`Phalcon\\Di\\InjectionAwareInterface <Phalcon_Di_InjectionAwareInterface>`, Serializable

Phalcon\\Mvc\\Model connects business objects and database tables to create a persistable domain model where logic and data are presented in one wrapping. It‘s an implementation of the object-relational mapping (ORM).  A model represents the information (data) of the application and the rules to manipulate that data. Models are primarily used for managing the rules of interaction with a corresponding database table. In most cases, each table in your database will correspond to one model in your application. The bulk of your application's business logic will be concentrated in the models.  Phalcon\\Mvc\\Model is the first ORM written in C-language for PHP, giving to developers high performance when interacting with databases while is also easy to use.  

.. code-block:: php

    <?php

     $robot = new Robots();
     $robot->type = 'mechanical';
     $robot->name = 'Astro Boy';
     $robot->year = 1952;
     if ($robot->save() == false) {
      echo "Umh, We can store robots: ";
      foreach ($robot->getMessages() as $message) {
    echo message;
      }
     } else {
      echo "Great, a new robot was saved successfully!";
     }



Constants
---------

*integer* **OP_NONE**

*integer* **OP_CREATE**

*integer* **OP_UPDATE**

*integer* **OP_DELETE**

*integer* **DIRTY_STATE_PERSISTENT**

*integer* **DIRTY_STATE_TRANSIENT**

*integer* **DIRTY_STATE_DETACHED**

Methods
-------

final public  **__construct** ([*unknown* $dependencyInjector], [*unknown* $modelsManager])

Phalcon\\Mvc\\Model constructor



public  **setDI** (*unknown* $dependencyInjector)

Sets the dependency injection container



public  **getDI** ()

Returns the dependency injection container



protected  **setEventsManager** (*unknown* $eventsManager)

Sets a custom events manager



protected  **getEventsManager** ()

Returns the custom events manager



public  **getModelsMetaData** ()

Returns the models meta-data service related to the entity instance



public  **getModelsManager** ()

Returns the models manager related to the entity instance



public  **setTransaction** (*unknown* $transaction)

Sets a transaction related to the Model instance 

.. code-block:: php

    <?php

    use Phalcon\Mvc\Model\Transaction\Manager as TxManager;
    use Phalcon\Mvc\Model\Transaction\Failed as TxFailed;
    
    try {
    
      $txManager = new TxManager();
    
      $transaction = $txManager->get();
    
      $robot = new Robots();
      $robot->setTransaction($transaction);
      $robot->name = 'WALL·E';
      $robot->created_at = date('Y-m-d');
      if ($robot->save() == false) {
    $transaction->rollback("Can't save robot");
      }
    
      $robotPart = new RobotParts();
      $robotPart->setTransaction($transaction);
      $robotPart->type = 'head';
      if ($robotPart->save() == false) {
    $transaction->rollback("Robot part cannot be saved");
      }
    
      $transaction->commit();
    
    } catch (TxFailed $e) {
      echo 'Failed, reason: ', $e->getMessage();
    }




protected  **setSource** (*unknown* $source)

Sets table name which model should be mapped



public  **getSource** ()

Returns table name mapped in the model



protected  **setSchema** (*unknown* $schema)

Sets schema name where table mapped is located



public  **getSchema** ()

Returns schema name where table mapped is located



public  **setConnectionService** (*unknown* $connectionService)

Sets the DependencyInjection connection service name



public  **setReadConnectionService** (*unknown* $connectionService)

Sets the DependencyInjection connection service name used to read data



public  **setWriteConnectionService** (*unknown* $connectionService)

Sets the DependencyInjection connection service name used to write data



public  **getReadConnectionService** ()

Returns the DependencyInjection connection service name used to read data related the model



public  **getWriteConnectionService** ()

Returns the DependencyInjection connection service name used to write data related to the model



public  **setDirtyState** (*unknown* $dirtyState)

Sets the dirty state of the object using one of the DIRTY_STATE_* constants



public  **getDirtyState** ()

Returns one of the DIRTY_STATE_* constants telling if the record exists in the database or not



public  **getReadConnection** ()

Gets the connection used to read data for the model



public  **getWriteConnection** ()

Gets the connection used to write data to the model



public :doc:`Phalcon\\Mvc\\Model <Phalcon_Mvc_Model>`  **assign** (*unknown* $data, [*unknown* $dataColumnMap], [*unknown* $whiteList])

Assigns values to a model from an array 

.. code-block:: php

    <?php

     $robot->assign(array(
    'type' => 'mechanical',
    'name' => 'Astro Boy',
    'year' => 1952
     ));
    
     //assign by db row, column map needed
     $robot->assign($dbRow, array(
    'db_type' => 'type',
    'db_name' => 'name',
    'db_year' => 'year'
     ));
    
     //allow assign only name and year
     $robot->assign($_POST, null, array('name', 'year');




public static :doc:`Phalcon\\Mvc\\Model <Phalcon_Mvc_Model>`  **cloneResultMap** (*unknown* $base, *unknown* $data, *unknown* $columnMap, [*unknown* $dirtyState], [*unknown* $keepSnapshots])

Assigns values to a model from an array returning a new model. 

.. code-block:: php

    <?php

    $robot = \Phalcon\Mvc\Model::cloneResultMap(new Robots(), array(
      'type' => 'mechanical',
      'name' => 'Astro Boy',
      'year' => 1952
    ));




public static *mixed*  **cloneResultMapHydrate** (*unknown* $data, *unknown* $columnMap, *unknown* $hydrationMode)

Returns an hydrated result based on the data and the column map



public static :doc:`Phalcon\\Mvc\\ModelInterface <Phalcon_Mvc_ModelInterface>`  **cloneResult** (:doc:`Phalcon\\Mvc\\ModelInterface <Phalcon_Mvc_ModelInterface>` $base, *unknown* $data, [*unknown* $dirtyState])

Assigns values to a model from an array returning a new model 

.. code-block:: php

    <?php

    $robot = Phalcon\Mvc\Model::cloneResult(new Robots(), array(
      'type' => 'mechanical',
      'name' => 'Astro Boy',
      'year' => 1952
    ));




public static :doc:`Phalcon\\Mvc\\Model\\ResultsetInterface <Phalcon_Mvc_Model_ResultsetInterface>`  **find** ([*unknown* $parameters])

Allows to query a set of records that match the specified conditions 

.. code-block:: php

    <?php

     //How many robots are there?
     $robots = Robots::find();
     echo "There are ", count($robots), "\n";
    
     //How many mechanical robots are there?
     $robots = Robots::find("type='mechanical'");
     echo "There are ", count($robots), "\n";
    
     //Get and print virtual robots ordered by name
     $robots = Robots::find(array("type='virtual'", "order" => "name"));
     foreach ($robots as $robot) {
       echo $robot->name, "\n";
     }
    
     //Get first 100 virtual robots ordered by name
     $robots = Robots::find(array("type='virtual'", "order" => "name", "limit" => 100));
     foreach ($robots as $robot) {
       echo $robot->name, "\n";
     }




public static :doc:`Phalcon\\Mvc\\Model <Phalcon_Mvc_Model>`  **findFirst** ([*unknown* $parameters])

Allows to query the first record that match the specified conditions 

.. code-block:: php

    <?php

     //What's the first robot in robots table?
     $robot = Robots::findFirst();
     echo "The robot name is ", $robot->name;
    
     //What's the first mechanical robot in robots table?
     $robot = Robots::findFirst("type='mechanical'");
     echo "The first mechanical robot name is ", $robot->name;
    
     //Get first virtual robot ordered by name
     $robot = Robots::findFirst(array("type='virtual'", "order" => "name"));
     echo "The first virtual robot name is ", $robot->name;




public static  **query** ([*unknown* $dependencyInjector])

Create a criteria for a specific model



protected *boolean*  **_exists** (*unknown* $metaData, *unknown* $connection, [*unknown* $table])

Checks if the current record already exists or not



protected static :doc:`Phalcon\\Mvc\\Model\\ResultsetInterface <Phalcon_Mvc_Model_ResultsetInterface>`  **_groupResult** (*unknown* $functionName, *unknown* $alias, *unknown* $parameters)

Generate a PHQL SELECT statement for an aggregate



public static *mixed*  **count** ([*unknown* $parameters])

Allows to count how many records match the specified conditions 

.. code-block:: php

    <?php

     //How many robots are there?
     $number = Robots::count();
     echo "There are ", $number, "\n";
    
     //How many mechanical robots are there?
     $number = Robots::count("type='mechanical'");
     echo "There are ", $number, " mechanical robots\n";




public static *mixed*  **sum** ([*unknown* $parameters])

Allows to calculate a summatory on a column that match the specified conditions 

.. code-block:: php

    <?php

     //How much are all robots?
     $sum = Robots::sum(array('column' => 'price'));
     echo "The total price of robots is ", $sum, "\n";
    
     //How much are mechanical robots?
     $sum = Robots::sum(array("type='mechanical'", 'column' => 'price'));
     echo "The total price of mechanical robots is  ", $sum, "\n";




public static *mixed*  **maximum** ([*unknown* $parameters])

Allows to get the maximum value of a column that match the specified conditions 

.. code-block:: php

    <?php

     //What is the maximum robot id?
     $id = Robots::maximum(array('column' => 'id'));
     echo "The maximum robot id is: ", $id, "\n";
    
     //What is the maximum id of mechanical robots?
     $sum = Robots::maximum(array("type='mechanical'", 'column' => 'id'));
     echo "The maximum robot id of mechanical robots is ", $id, "\n";




public static *mixed*  **minimum** ([*unknown* $parameters])

Allows to get the minimum value of a column that match the specified conditions 

.. code-block:: php

    <?php

     //What is the minimum robot id?
     $id = Robots::minimum(array('column' => 'id'));
     echo "The minimum robot id is: ", $id;
    
     //What is the minimum id of mechanical robots?
     $sum = Robots::minimum(array("type='mechanical'", 'column' => 'id'));
     echo "The minimum robot id of mechanical robots is ", $id;




public static *double*  **average** ([*unknown* $parameters])

Allows to calculate the average value on a column matching the specified conditions 

.. code-block:: php

    <?php

     //What's the average price of robots?
     $average = Robots::average(array('column' => 'price'));
     echo "The average price is ", $average, "\n";
    
     //What's the average price of mechanical robots?
     $average = Robots::average(array("type='mechanical'", 'column' => 'price'));
     echo "The average price of mechanical robots is ", $average, "\n";




public  **fireEvent** (*unknown* $eventName)

Fires an event, implicitly calls behaviors and listeners in the events manager are notified



public  **fireEventCancel** (*unknown* $eventName)

Fires an event, implicitly calls behaviors and listeners in the events manager are notified This method stops if one of the callbacks/listeners returns boolean false



protected  **_cancelOperation** ()

Cancel the current operation



public  **appendMessage** (*unknown* $message)

Appends a customized message on the validation process 

.. code-block:: php

    <?php

     use \Phalcon\Mvc\Model\Message as Message;
    
     class Robots extends \Phalcon\Mvc\Model
     {
    
       public function beforeSave()
       {
     if ($this->name == 'Peter') {
    	$message = new Message("Sorry, but a robot cannot be named Peter");
    	$this->appendMessage($message);
     }
       }
     }




protected  **validate** (*unknown* $validator)

Executes validators on every validation call 

.. code-block:: php

    <?php

    use Phalcon\Mvc\Model\Validator\ExclusionIn as ExclusionIn;
    
    class Subscriptors extends \Phalcon\Mvc\Model
    {
    
    public function validation()
      {
     		$this->validate(new ExclusionIn(array(
    		'field' => 'status',
    		'domain' => array('A', 'I')
    	)));
    	if ($this->validationHasFailed() == true) {
    		return false;
    	}
    }
    }




public  **validationHasFailed** ()

Check whether validation process has generated any messages 

.. code-block:: php

    <?php

    use Phalcon\Mvc\Model\Validator\ExclusionIn as ExclusionIn;
    
    class Subscriptors extends \Phalcon\Mvc\Model
    {
    
    public function validation()
      {
     		$this->validate(new ExclusionIn(array(
    		'field' => 'status',
    		'domain' => array('A', 'I')
    	)));
    	if ($this->validationHasFailed() == true) {
    		return false;
    	}
    }
    }




public  **getMessages** ([*unknown* $filter])

Returns all the validation messages 

.. code-block:: php

    <?php

    $robot = new Robots();
    $robot->type = 'mechanical';
    $robot->name = 'Astro Boy';
    $robot->year = 1952;
    if ($robot->save() == false) {
      	echo "Umh, We can't store robots right now ";
      	foreach ($robot->getMessages() as $message) {
    		echo $message;
    	}
    } else {
      	echo "Great, a new robot was saved successfully!";
    }




protected  **_checkForeignKeysRestrict** ()

Reads "belongs to" relations and check the virtual foreign keys when inserting or updating records to verify that inserted/updated values are present in the related entity



protected  **_checkForeignKeysReverseCascade** ()

Reads both "hasMany" and "hasOne" relations and checks the virtual foreign keys (cascade) when deleting records



protected  **_checkForeignKeysReverseRestrict** ()

Reads both "hasMany" and "hasOne" relations and checks the virtual foreign keys (restrict) when deleting records



protected  **_preSave** (*unknown* $metaData, *unknown* $exists, *unknown* $identityField)

Executes internal hooks before save a record



protected  **_postSave** (*unknown* $success, *unknown* $exists)

Executes internal events after save a record



protected *boolean*  **_doLowInsert** (*unknown* $metaData, *unknown* $connection, *unknown* $table, *unknown* $identityField)

Sends a pre-build INSERT SQL statement to the relational database system



protected *boolean*  **_doLowUpdate** (*unknown* $metaData, *unknown* $connection, *unknown* $table)

Sends a pre-build UPDATE SQL statement to the relational database system



protected *boolean*  **_preSaveRelatedRecords** (*unknown* $connection, *unknown* $related)

Saves related records that must be stored prior to save the master record



protected *boolean*  **_postSaveRelatedRecords** (*unknown* $connection, *unknown* $related)

Save the related records assigned in the has-one/has-many relations



public *boolean*  **save** ([*unknown* $data], [*unknown* $whiteList])

Inserts or updates a model instance. Returning true on success or false otherwise. 

.. code-block:: php

    <?php

    //Creating a new robot
    $robot = new Robots();
    $robot->type = 'mechanical';
    $robot->name = 'Astro Boy';
    $robot->year = 1952;
    $robot->save();
    
    //Updating a robot name
    $robot = Robots::findFirst("id=100");
    $robot->name = "Biomass";
    $robot->save();




public  **create** ([*unknown* $data], [*unknown* $whiteList])

Inserts a model instance. If the instance already exists in the persistance it will throw an exception Returning true on success or false otherwise. 

.. code-block:: php

    <?php

    //Creating a new robot
    $robot = new Robots();
    $robot->type = 'mechanical';
    $robot->name = 'Astro Boy';
    $robot->year = 1952;
    $robot->create();
    
      //Passing an array to create
      $robot = new Robots();
      $robot->create(array(
      'type' => 'mechanical',
      'name' => 'Astroy Boy',
      'year' => 1952
      ));




public  **update** ([*unknown* $data], [*unknown* $whiteList])

Updates a model instance. If the instance doesn't exist in the persistance it will throw an exception Returning true on success or false otherwise. 

.. code-block:: php

    <?php

    //Updating a robot name
    $robot = Robots::findFirst("id=100");
    $robot->name = "Biomass";
    $robot->update();




public  **delete** ()

Deletes a model instance. Returning true on success or false otherwise. 

.. code-block:: php

    <?php

    $robot = Robots::findFirst("id=100");
    $robot->delete();
    
    foreach (Robots::find("type = 'mechanical'") as $robot) {
       $robot->delete();
    }




public  **getOperationMade** ()

Returns the type of the latest operation performed by the ORM Returns one of the OP_* class constants



public  **refresh** ()

Refreshes the model attributes re-querying the record from the database



public  **skipOperation** (*unknown* $skip)

Skips the current operation forcing a success state



public  **readAttribute** (*unknown* $attribute)

Reads an attribute value by its name 

.. code-block:: php

    <?php

     echo $robot->readAttribute('name');




public  **writeAttribute** (*unknown* $attribute, *unknown* $value)

Writes an attribute value by its name 

.. code-block:: php

    <?php

     	$robot->writeAttribute('name', 'Rosey');




protected  **skipAttributes** (*unknown* $attributes)

Sets a list of attributes that must be skipped from the generated INSERT/UPDATE statement 

.. code-block:: php

    <?php

    <?php
    
    class Robots extends \Phalcon\Mvc\Model
    {
    
       public function initialize()
       {
       $this->skipAttributes(array('price'));
       }
    }




protected  **skipAttributesOnCreate** (*unknown* $attributes)

Sets a list of attributes that must be skipped from the generated INSERT statement 

.. code-block:: php

    <?php

    <?php
    
    class Robots extends \Phalcon\Mvc\Model
    {
    
       public function initialize()
       {
       $this->skipAttributesOnCreate(array('created_at'));
       }
    }




protected  **skipAttributesOnUpdate** (*unknown* $attributes)

Sets a list of attributes that must be skipped from the generated UPDATE statement 

.. code-block:: php

    <?php

    <?php
    
    class Robots extends \Phalcon\Mvc\Model
    {
    
       public function initialize()
       {
       $this->skipAttributesOnUpdate(array('modified_in'));
       }
    }




protected  **allowEmptyStringValues** (*unknown* $attributes)

Sets a list of attributes that must be skipped from the generated UPDATE statement 

.. code-block:: php

    <?php

    <?php
    
    class Robots extends \Phalcon\Mvc\Model
    {
    
       public function initialize()
       {
       $this->allowEmptyStringValues(array('name'));
       }
    }




protected  **hasOne** (*unknown* $fields, *unknown* $referenceModel, *unknown* $referencedFields, [*unknown* $options])

Setup a 1-1 relation between two models 

.. code-block:: php

    <?php

    <?php
    
    class Robots extends \Phalcon\Mvc\Model
    {
    
       public function initialize()
       {
       $this->hasOne('id', 'RobotsDescription', 'robots_id');
       }
    }




protected  **belongsTo** (*unknown* $fields, *unknown* $referenceModel, *unknown* $referencedFields, [*unknown* $options])

Setup a relation reverse 1-1  between two models 

.. code-block:: php

    <?php

    <?php
    
    class RobotsParts extends \Phalcon\Mvc\Model
    {
    
       public function initialize()
       {
       $this->belongsTo('robots_id', 'Robots', 'id');
       }
    
    }




protected  **hasMany** (*unknown* $fields, *unknown* $referenceModel, *unknown* $referencedFields, [*unknown* $options])

Setup a relation 1-n between two models 

.. code-block:: php

    <?php

    <?php
    
    class Robots extends \Phalcon\Mvc\Model
    {
    
       public function initialize()
       {
       $this->hasMany('id', 'RobotsParts', 'robots_id');
       }
    }




protected :doc:`Phalcon\\Mvc\\Model\\Relation <Phalcon_Mvc_Model_Relation>`  **hasManyToMany** (*unknown* $fields, *unknown* $intermediateModel, *unknown* $intermediateFields, *unknown* $intermediateReferencedFields, *unknown* $referenceModel, *unknown* $referencedFields, [*unknown* $options])

Setup a relation n-n between two models through an intermediate relation 

.. code-block:: php

    <?php

    <?php
    
    class Robots extends \Phalcon\Mvc\Model
    {
    
       public function initialize()
       {
       //Setup a many-to-many relation to Parts through RobotsParts
       $this->hasManyToMany(
    		'id',
    		'RobotsParts',
    		'robots_id',
    		'parts_id',
    		'Parts',
    		'id'
    	);
       }
    }




public  **addBehavior** (*unknown* $behavior)

Setups a behavior in a model 

.. code-block:: php

    <?php

    <?php
    
    use Phalcon\Mvc\Model\Behavior\Timestampable;
    
    class Robots extends \Phalcon\Mvc\Model
    {
    
       public function initialize()
       {
    	$this->addBehavior(new Timestampable(array(
    		'onCreate' => array(
    			'field' => 'created_at',
    			'format' => 'Y-m-d'
    		)
    	)));
       }
    }




protected  **keepSnapshots** (*unknown* $keepSnapshot)

Sets if the model must keep the original record snapshot in memory 

.. code-block:: php

    <?php

    <?php
    
    class Robots extends \Phalcon\Mvc\Model
    {
    
       public function initialize()
       {
    	$this->keepSnapshots(true);
       }
    }




public  **setSnapshotData** (*unknown* $data, [*unknown* $columnMap])

Sets the record's snapshot data. This method is used internally to set snapshot data when the model was set up to keep snapshot data



public  **hasSnapshotData** ()

Checks if the object has internal snapshot data



public  **getSnapshotData** ()

Returns the internal snapshot data



public  **hasChanged** ([*unknown* $fieldName])

Check if a specific attribute has changed This only works if the model is keeping data snapshots



public  **getChangedFields** ()

Returns a list of changed values



protected  **useDynamicUpdate** (*unknown* $dynamicUpdate)

Sets if a model must use dynamic update instead of the all-field update 

.. code-block:: php

    <?php

    <?php
    
    class Robots extends \Phalcon\Mvc\Model
    {
    
       public function initialize()
       {
    	$this->useDynamicUpdate(true);
       }
    }




public :doc:`Phalcon\\Mvc\\Model\\ResultsetInterface <Phalcon_Mvc_Model_ResultsetInterface>`  **getRelated** (*unknown* $alias, [*unknown* $arguments])

Returns related records based on defined relations



protected *mixed*  **_getRelatedRecords** (*unknown* $modelName, *unknown* $method, *unknown* $arguments)

Returns related records defined relations depending on the method name



public *mixed*  **__call** (*unknown* $method, *unknown* $arguments)

Handles method calls when a method is not implemented



public static *mixed*  **__callStatic** (*unknown* $method, [*unknown* $arguments])

Handles method calls when a static method is not implemented



public  **__set** (*unknown* $property, *unknown* $value)

Magic method to assign values to the the model



public :doc:`Phalcon\\Mvc\\Model\\Resultset <Phalcon_Mvc_Model_Resultset>` |Phalcon\Mvc\Model **__get** (*unknown* $property)

Magic method to get related records using the relation alias as a property



public  **__isset** (*unknown* $property)

Magic method to check if a property is a valid relation



public  **serialize** ()

Serializes the object ignoring connections, services, related objects or static properties



public  **unserialize** (*unknown* $data)

Unserializes the object from a serialized string



public  **dump** ()

Returns a simple representation of the object that can be used with var_dump 

.. code-block:: php

    <?php

     var_dump($robot->dump());




public *array*  **toArray** ([*array* $columns])

Returns the instance as an array representation 

.. code-block:: php

    <?php

     print_r($robot->toArray());




public static  **setup** (*unknown* $options)

Enables/disables options in the ORM



public  **reset** ()

Reset a model instance data



