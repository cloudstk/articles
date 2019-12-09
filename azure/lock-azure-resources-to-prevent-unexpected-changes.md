Lock Azure resources to prevent unexpected changes
=================================================
Locks allow us to control access to our subscription, resource group or individual resource. The lock
helps to prevent other users from accidental deletion or modification of resources.

Locks have a parent-child relationship. When you apply a lock at a parent scope, this will affect all the resouces within scope.

There are two types of resource locks that can be applied:
----------------------------------------------------------
* CanNotDelete - The resource can be read and modified, but not deleted the resource.
* ReadOnly - The resource can Read but not modify, delete or update the resource.

Locks can be assigned by using one of the following:
* Azure Portal
* PowerShell
* Azure CLI
* Template
* Rest API

In the video below, you will see how to lock a resouce group from the Azure Portal. 

[![Lock azure resources](http://img.youtube.com/vi/mDOOKrEXAZY/0.jpg)](http://www.youtube.com/watch?v=mDOOKrEXAZY "Lock Azure resources to prevent unexpected changes")

----------------------
In this article, we have looked at How to add a lock to a resouce from the Azure Portal and we have also seen a Warning message when we tried to delete it.
