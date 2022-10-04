 

### JSON Syntax Review

**JSON**  

* stands for **J**ava**S**cript **O**bject **N**otation
* is a text-data interchange format
* is similar to xml, but more compact and easier to read

**JSON Parser:**  
A JSON parser is a program or module of a program that reads JSON format text for use in software such as MongoDB.  A JSON parser can be written in any programming language.  A list of available parsers are listed on [http://www.json.org/](http://www.json.org/).  
  
**A JSON Document consists of the following structures:**  

**Values:** A value can be any of the following:

**String:** text surrounded by double quotes.    Note: single quotes are usually allowed by parsers (such as MongoDB's parser), but is not actually part of the valid JSON format specification.  For example these are all json string values:

  * **"**a string value"
  * "another-value"
  * "value"

**Number:** Numbers for example:

  * 10
  * 1.0
  * -12
  * -12.05
  * 1.5e2
  * 1.5e+2
  * 1.5e-2
  * 1.5E2
  * 1.5E+2
  * 1.5E-2

**true** or **false**: The boolean values of _true_ or _false_.
**null**: Null basically denotes a non-value.
**Object:** See below for definition.
**Array:**  See below for definition.

**Name/Value pairs or Properties:**

* A name/value pair consists of a _string_, a colon ':' then a _value_ (see above for definition of string and value).  For example:

* "name" : "value"
* "count" : 5
* "isTrueOrFalse" : false

**Objects:**

* An object is a collection of _name/value pairs_ surrounded by curly braces { }.  The name/value pairs in the object are separated by commas.  For example:

* {"name" : "value"}
* {"name" : "value", "num" : 5 }

**Arrays:**

* A list, is a collection of _objects_ and/or _values_ surrounded by brackets \[ \].  Items in the list are separated by commas.  For example:

  * \[5\]
  * \[{"name", "value"}\]
  * \[{"name": "value"}, { "number": 10}, "string value", 20\]

See [here for the official specification](http://json.org/).  
  
**JSON Sample Documents:**  
See [here for sample JSON documents](http://json.org/example.html).  
  
**Editing JSON:**  
[JSONLint](http://jsonlint.com/) is a great tool for validating your JSON documents: [http://jsonlint.com/](http://jsonlint.com/)  
**MongoDB and JSON:**  
MongoDB shell uses an extended JSON format.  See here for some details on this topic: [http://www.mongodb.org/display/DOCS/Mongo+Extended+JSON](http://www.mongodb.org/display/DOCS/Mongo+Extended+JSON)  
  
Internally MongoDB stores data in BSON format or Binary JSON.  See here for specification details: [http://bsonspec.org/](http://bsonspec.org/)
