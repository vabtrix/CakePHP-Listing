#CakePHP-Listing
Model behaviour to append an optgroup into a list for a select box. The idea for this behaviour is that if you have a list of items which belong to another model, it will include that models name.

So we change,  

```
array(
  1 => 'First',
  2 => 'Second'
);
```  
..into this..

```
array(
  'Cats' => array(
    1 => 'First',
  ),
  'Dogs' => array(
    2 => 'Second'
  )
);
```  

..and you should end up with nice option groups in your selects.
![Select box with optgroup](http://i.imgur.com/QP7BhMl.png)

#Version
This is something I'd consider `alpha`. It works for me in a few projects, but it's not been extensivly tested.

#Installation
This is a standard CakePHP plugin, so it will need to extracted or submoduled into your `app/Plugin` folder. I call it `Listing`, so it should live in `app/Plugin/Listing`.

You will need to activate the plugin in your `app/Config/bootstrap.php` using `CakePlugin::load('Listing')`, unless you are already using `CakePlugin::loadAll()`

#Requirements
* Cake 2  
* Containable  
The models you are using with this behaviour must have Containable enabled.  
`public $actsAs = array('Containable', 'Listing.Listable');`  
I tend to add Containable to my AppModel as it's handy to have everywhere!

#Usage
You can attach to the model using the `$actsAs` array. As you would normally. You **must** include the name of the related model that you want to join to when you configure the behaviour.  

You can also specify the fields that you want to use using, `primaryKey` and `displayField`.  

```
public $actsAs = array(
    'Listing.Listable' => array(
       'relatedModelName' => 'Provider',
       'relatedPrimaryKey' => 'id', // optional - default shown
       'relatedDisplayField' => 'name', // optional - default shown
    )
);
```

[More on Behaviours in the Book](http://book.cakephp.org/2.0/en/models/behaviors.html).

Then in order to attach the extra model, I have implemented a custom find called `listing` which will return the formatted list.  

For example,
`$broadbands = $this->Package->Broadband->find('listing');`  

#Todo
* Write some tests
* Tidy up the source a little
* Look to refactor
* Rewrite this README file!
