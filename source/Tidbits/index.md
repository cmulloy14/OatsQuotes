---
title: iOS Tidbits
date: 2019-12-02 22:44:47
---


** Tidbit #2 -- type(of:) vs 'is'  **
I recently ran in to code that used **type(of:)** to compare the types of two objects. This code failed when I changed one object to be optional.
This was strange to me, considering it seemed that an object and an optional object of the same type should be the same type, right?  
Turns out, **type(of:)** returns the type of the object at runtime, and an optional is actually an Optional type with that type as its wrapped value.  
The better option in this case is to use **is** to check the type, becuase I really only wanted to know the subclass of the object. 
**is** returns whether the object is a subclass of the specified type. Check out the behavior below.

{% codeblock lang:swift line_number:false %}

let string = "non-optional"
let optionalString: String? = "optional"
let nilString: String? = nil

type(of: string) // String.Type
type(of: optionalString) // Optional<String>.Type
type(of: nilString) // Optional<String>.Type

string is String // true - warning: 'is' test is always true
optionalString is String // true 
nilString is String // false 

/*  

 Last two 'is' check warnings: 
 Checking a value with optional type 'String?' against dynamic type 'String' succeeds whenever the value is non-nil; 
 did you mean to use '!= nil'?
 Replace 'is String' with '!= nil'
 */ 


{% endcodeblock %}

It's important to note how **is** behaves with optionals; it basically turns in to a nil check. 
Some interesting, not so obvious behavior.

<br/>
<br/>

---

<br/>



** Tidbit #1 -- Defer vs Return: Execution Order **

According to swift.org, "A **defer** statement is used for executing code just before transferring program control outside of the scope that the defer statement appears in."
 
So we often see **defer** at the beggining of a method, containing some sort of clean-up actions that will be perofrmed before the function is finished. This is helpful when there are multiple **return** statments in a method, that are perhaps nested in an if/else if/else chain or a switch statment, so we don't have to duplicate clean-up code. 

But exactly when the **defer** block executes is not neccesarily intuitive. I found myself wondering, what happens first: the code in a defer block, or the code in a return statement? I ran the following code to find out: 

{% codeblock lang:swift line_number:false %}
func test() {
    defer {
        print("deferred")
    }
    return print("returned")
}

test()
{% endcodeblock %}

Output:
{% codeblock lang:swift line_number:false %}
returned
deferred
{% endcodeblock %}

I've always hought a **return** statement is the last thing executed in a Swift function, but it turns out **defer** executes even after **return**. So this is a good little tidbit to keep in mind when using **defer** in your Swift functions. 
