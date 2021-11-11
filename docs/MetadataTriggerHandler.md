---
layout: default
---

# MetadataTriggerHandler class

This class exists as a unified, trigger handler class. It uses Custom Metadata, and introspection of the Trigger.new variable to determine what trigger handler classes should be called, and in what order. Metadata*Driven_Trigger**mdt has three fields: Object**c - is a metadata entity look up to an sObject ie: Account Execution_Order**c - is an integer and determines the order the trigger handlers are executed Class**c - is a String holding the name of the Trigger Handler to execute Note: This Trigger framework works like this: An .trigger for a sObject invokes this class via: new MetadataTriggerHandler().run(); This trigger handler class extends TriggerHandler - all the trigger handler classes \_must* extend trigger handler. Most classes will only overwrite the context methods like afterUpdate(). This class, however, overrides the run method. This class is responsible for determining which other trigger handler classes to instantiate and run. Concrete example: AccountTrigger.trigger (in this org) - invokes this class. This class queries the custom metadata and will find (at least) one metadata record tied to Account and the metadata record&apos;s Class\_\_c specifies AccountTriggerHandler. This class then loops over the returned metadata records, instantiating the classes specified. It then calls the appropriate context methods on those classes. Note: The TriggerHandler framework below does _not_ give you the ability to order, or re-arrange the trigger work of managed packages. It also does not allow you to declare the _order of methods_ within the triggerHandler classes themselves. When using the MetadataTriggerHandler, it&apos;s better to have a high number of singularly focused trigger handler classes than a few classes with multiple methods.

---

## Constructors

### `MetadataTriggerHandler()`

Constructor used by live triggers.

### `MetadataTriggerHandler(MetadataTriggerService mts)`

---

## Properties

### `activeHandler` → `TriggerHandler`

### `mts` → `MetadataTriggerService`

### `tryggers` → `List<Metadata_Driven_Trigger__mdt>`

---

## Methods

### `getInstance()` → `MetadataTriggerHandler`

MetadataTriggerHandler.getInstance().setMTS(mtsInstance)

### `run()` → `void`

Overrides the standard Run() method, which allows this metadata based trigger handler can be an incremental update / sit beside other trigger handlers classes that are directly invoked by a trigger

### `setMTS(MetadataTriggerService mtsInstance)` → `MetadataTriggerHandler`

---
