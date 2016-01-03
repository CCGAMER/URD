# URD
#Undo Redo Pattern for C# applications


This is a basic undo pattern for .NET applications which is developed for the use in the project GS Subtitle (not published). 
In this pattern when you want a undo / redo able action you will need to warp that action with using statement.
As an example if you going to change a property, you can do this:
```C#
using (new PropertyChange(Object, "Property", "Property changed "))
{
  Object.Property="new value";
}
```
Now the change you made to the "Property" property of the "Object" object is added to the drop out stack and it can undo or redo any time you want.

if you want a undoAble list change you can do it using same syntax:

```C#
private void AddNewItem(<string>List list,string item,bool undoAble)
{
	using (undoAble?new ListChangeAddElement(list,item,"add new string to the string list"):null) //you can use a condition then you can minimize code
	{
		list.Add(item);
	}
}
```
Removing a Item:
```C#
private void RemoveItem(list,item,bool undoAble)
{
	using(undoAble?new ListChangeRemoveElement(list,item,list.IndexOf(item)," remove "+item+" from the string list"))
	{
		list.Remove(item);
	}
}
```
And So on.. (check the code)

Benifits of this Pattern

<b>Low CPU and Memory Usage<b/>
Undo only what you want</b>

<b>if you want to implement your own operation . only thing you need to do is create a class--> extend Change class and IUndoAble interface.</b> 


