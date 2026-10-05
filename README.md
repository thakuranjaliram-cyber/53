# 53

**pt2**
Update the country to UK for all female users. 
db.col.updateMany({Gender:"Female"},{$set:{Country:"UK"}})

5. Add the new field company to all the documents.
   db.col.updateMany({},{$set:{Company:"Wipro"}})

6. Delete all the documents where Gender = ‘M’.
   db.col.remove({"Gender":"Male"})
 
1. Find out a count of female users who stay in either India or USA.
 db.col.find({$or:[{Country:"India"},{Country:"USA"}],Gender:"Female"}).count()

2. Display the first name and age of all female employees.
   db.col.find({Gender:"Female"},{Name:1,Age:1})


   **pt3 Aggregate()**
   
1. Group by function to get count.
   db.col.aggregate([{$group:{_id:"$City",cityCount:{$sum:1}}}])
3. Sum function.
    db.col.aggregate([{$group:{_id:"$City",cityCount:{$sum:$Salary}}}])
5. Avg function.
    db.col.aggregate([{$group:{_id:"$City",cityCount:{$avg:"$Salary"}}}])
1. Min function
   db.col.aggregate([{$group:{_id:"$City",cityCount:{$min:"$Salary"}}}])
3. Max function.
   db.col.aggregate([{$group:{_id:"$City",cityCount:{$max:"$Salary"}}}])
5. First function
   db.col.aggregate([{$group:{_id:"$City",cityCount:{$first:"$Salary"}}}])
7. Last function
   db.col.aggregate([{$group:{_id:"$City",cityCount:{$last:"$Salary"}}}])
9. Push function
    db.col.aggregate([{$group:{_id:"$City",cityCount:{$push:"$Salary"}}}])
11. addToSet function
    db.col.aggregate([{$group:{_id:"$City",cityCount:{$addToSet:"Salary"}}}])




    **pt4 Java**
1. Insert the document in MongoDB using Java.
   
import com.mongodb.client.MongoCollection; 
import com.mongodb.client.MongoDatabase; 
import com.mongodb.MongoClient; 
import org.bson.Document; 
public class insert 
{ 
public static void main(String[] args) 
{ 
MongoClient mongo = new MongoClient("localhost",27017); 
System.out.println("Connected to the database successfully."); 
MongoDatabase database = mongo.getDatabase("TYITDB239720"); 
MongoCollection<Document> collection = database.getCollection("myCol"); 
System.out.println("Collection myCol selected successfully"); 
Document document = new Document(); 
document.append("id",1); 
document.append("Name","Romal"); 
document.append("RollNo",239720); 
document.append("Age",20); 
document.append("College","MCC"); 
collection.insertOne(document); 
System.out.println("Document inserted successfully"); 
} 
}

3. Update the document in MongoDB using Java.
   
import com.mongodb.DB; 
import com.mongodb.DBCollection; 
import com.mongodb.BasicDBObject; 
import com.mongodb.MongoClient; 
import com.mongodb.WriteResult; 
import java.net.UnknownHostException; 
public class update 
{ 
public static void main(String[] args) 
{ 
MongoClient mongo = new MongoClient("localhost",27017); 
System.out.println("Connected to the database successfully."); 
DB db = mongo.getDB("TYITDB239720"); 
DBCollection col = db.getCollection("myCol"); 
BasicDBObject query = new BasicDBObject("id",1); 
BasicDBObject update = new BasicDBObject(); 
update.put("$set",new BasicDBObject("Age",27)); 
WriteResult result = col.update(query,update); 
mongo.close(); 
} 
} 


4. Retrieve the document in MongoDB using Java
   
import com.mongodb.client.MongoCollection; 
import com.mongodb.client.MongoDatabase; 
import com.mongodb.MongoClient; 
import com.mongodb.MongoCredential; 
import org.bson.Document; 
import java.util.Iterator; 
import com.mongodb.client.FindIterable; 
public class retrieve 
{ 
public static void main(String[] args) 
{ 
MongoClient mongo = new MongoClient("localhost",27017); 
System.out.println("Connected to the database successfully."); 
MongoDatabase database = mongo.getDatabase("TYITDB239720"); 
MongoCollection<Document> collection = database.getCollection("myCol"); 
System.out.println("Collection myCol selected successfully"); 
FindIterable<Document> iterDoc = collection.find(); 
int i = 1; 
Iterator it = iterDoc.iterator(); 
while(it.hasNext()) 
{ 
System.out.println(it.next()); 
i++; 
} 
} 
} 

3.Delete the document in MongoDB using Java.

import com.mongodb.client.MongoCollection; 
import com.mongodb.client.MongoDatabase; 
import com.mongodb.MongoClient; 
import com.mongodb.MongoCredential; 
import org.bson.Document; 
import com.mongodb.client.model.Filters; 
public class delete 
{ 
public static void main(String[] args) 
{ 
MongoClient mongo = new MongoClient("localhost",27017); 
System.out.println("Connected to the database successfully."); 
MongoDatabase database = mongo.getDatabase("TYITDB239720"); 
MongoCollection<Document> collection = database.getCollection("myCol"); 
System.out.println("Collection myCol selected successfully"); 
collection.deleteOne(Filters.eq("id",1)); 
System.out.println("Document deleted successfully"); 
} 
}


**Practical 5 – PHP**
php_mongo.dll ---> copy this file and paste it in xampp--> php--> ext

Edit the configuration --> xampp --> php ---> php(Type: Configuration setting)

Save Files at the location: C:\xampp\htdocs

Execute: Open xampp Apache → Start (Make it active) and Admin(Make it active)

Browser will open

Remove dashboard and instead give the name of the file (eg: insert.php)

Output is printed.

1. insert.php
<?php $m = new MongoClient(); echo "Connection to database successfully"; $db = $m -> MYDB239720; echo "\nDatabase selected successfully"; $col = $db -> MyCol; echo "\nCollection selected successfully"; $doc = array( "name" => "Romal", "age" => 20, "dept" => "TYIT", "rollno" => 239720 ); $col -> insert($doc); echo "\nDocument inserted successfully"; ?>

Output:
Connection to database successfully
Database selected successfully
Collection selected successfully
Document inserted successfully

2. update.php
<?php $m = new MongoClient(); echo "Connection to database successfully"; $db = $m -> MYDB239720; echo "\nDatabase selected successfully"; $col = $db -> MyCol; echo "\nCollection selected successfully"; $col -> update(array( "name" => "Romal"),array('$set'=>array("age" => 19))); echo "\nDocument updated successfully"; ?>

Output:
Connection to database successfully
Database selected successfully
Collection selected successfully
Document updated successfully

3. retrieve.php
<?php $m = new MongoClient(); echo "Connection to database successfully"; $db = $m -> MYDB239720; echo "\nDatabase selected successfully"; $col = $db -> MyCol; echo "\nCollection selected successfully"; $cursor = $col -> find(); foreach($cursor as $doc) { echo"<br/>"; echo $doc["name"]."<br/>"; echo $doc["age"]."<br/>"; echo $doc["dept"]."<br/>"; echo $doc["rollno"]."<br/>"; }?>

Output:
Connection to database successfully
Database selected successfully
Collection selected successfully

Romal
20
TYIT
239720

4. delete.php
<?php $m = new MongoClient(); echo "Connection to database successfully"; $db = $m -> MYDB239720; echo "\nDatabase selected successfully"; $col = $db -> MyCol; echo "\nCollection selected successfully"; $col -> remove(array( "name" => "Romal")); echo "\nDocument deleted successfully"; ?>

Output:
Connection to database successfully
Database selected successfully
Collection selected successfully
Document deleted successfully



**6.Python**
1. insert 
6.Python 
from pymongo import MongoClient 
client = MongoClient('localhost',27017) 
db = client.TYITDB239720 
def insert(): 
try: 
name1 = input("Enter the Name:") 
age1 = input("Enter the Age:") 
dept1 = input("Enter the Department:") 
pin1 = input("Enter the Pin No:") 
db.MyCol.insert_one({ 
"name":name1, 
"age":age1, 
"dept":dept1, 
"pin":pin1 
}) 
print("Inserted data successfully") 
except Exception: 
print(str(e)) 
insert()

2. update() 
from pymongo import MongoClient 
client = MongoClient('localhost',27017) 
db = client.TYITDB239720 
def update(): 
try: 
name1 = input("Enter the Name:") 
age1 = input("Enter the Age to update:") 
db.MyCol.update_one({"name":name1},{"$set":{"age":age1}}) 
print("\nRecords updated successfully\n") 
except Exception: 
print(str(e)) 
update()

3. Retrieve
from pymongo import MongoClient 
client = MongoClient('localhost',27017) 
db = client.TYITDB239720 
def read(): 
try: 
Col = db.MyCol.find() 
print("\nAll data from database TYITDB239720:") 
for MyCol in Col: 
print(MyCol) 
except Exception: 
print(str(e)) 
read()


4. delete 
from pymongo import MongoClient 
client = MongoClient('localhost',27017) 
db = client.TYITDB239720
def delete(): 
try: 
name1 = input("Enter the name:") 
db.MyCol.delete_one({"name":name1}) 
print("\nData deleted successfully") 
except Exception: 
print(str(e)) 
delete()




**Practical 7 **
1. Write a jQuery to check the contents of the elements on the 
button click. 
<!DOCTYPE html> 
<head> 
<title>Basic jQuery</title> 
<script src="jquery-3.6.1.min.js"></script> 
<script> 
$(document).ready(function () { 
$("#btn").click(function(){ 
document.write("Hello Romal") 
}) 
}) 
</script> 
</head> 
<body> 
<p>Romal: 239720</p> 
<button id="btn">Click Me</button> 
</body>



2. Write a jQuery to select elements by class name, id and element 
names. 
<!DOCTYPE html> 
<head> 
<title>Basic jQuery</title> 
<script src="jquery-3.6.1.min.js"></script> 
<script> 
$(document).ready(function() { 
$(".class1").css("background","lightblue"); 
$("#id1").css("background","pink"); 
$("h2").css("background", "lightgreen"); 
}) 
</script> 
</head> 
<body> 
<p class="class1">Romal: 239720</p> 
<p id="id1">Romal Shah</p> 
<h2>Welcome Romal</h2> 
</body>


3. Write jQuery to show the use of click(), hover(), on(), 
trigger(),off() events. 
 
<!DOCTYPE html> 
<head> 
    <title>Basic jQuery</title> 
    <script src="jquery-3.6.1.min.js"></script> 
    <script> 
        $(document).ready(function () { 
            $("#b1").hover (function(){ 
            document.write("Hello Romal") 
            }) 
            $("p").on("click", function() { 
                $(this).css("background", "yellow"); 
            }); 
            $("#b2").click(function(){ 
                $("p").off("click"); 
            }); 
            $("#b3").on(function(){ 
                $("#t1").hide(); 
            }); 
            $("input").select(function(){ 
                $("input").after("Text Marked!") 
            }); 
            $("#b4").click(function(){ 
                $("input").trigger("select"); 
            }); 
        }) 
    </script> 
</head> 
<body> 
    <button id="b1">Hover</button><br>
<p>Welcome to the Mulund College</p><br> 
<p>Romal: 239720</p><br> 
<button id="b2">Off</button><br> 
<p id="t1">Hello Romal</p><br> 
<button id="b3">On</button><br> 
<input type="text" value="Romal 239720"><br> 
<button id="b4">Trigger</button><br> 
</body>


1. Write a jQuery to create animated show hide effect. 
<!DOCTYPE html> 
<head> 
<title>Basic jQuery</title> 
<script src="jquery-3.6.1.min.js"></script> 
<script> 
$(document).ready(function(){ 
$("#b1").click(function(){ 
$("p").hide(); 
}); 
$("#b2").click(function(){  
$("p").show(); 
}) 
}) 
</script> 
</head>
<body> 
<p>Romal Shah:239720</p> 
<button id="b1">Hide</button> 
<button id="b2">Show</button> 
</body>



1. Write a jQuery to create a simple toggle effect. 
<!DOCTYPE html> 
<head> 
<title>Basic jQuery</title> 
<script src="jquery-3.6.1.min.js"></script> 
<script> 
$(document).ready(function(){ 
$("button").click(function(){ 
$("p").toggle(); 
}); 
}) 
</script> 
</head> 
<body> 
<p>Romal Shah:239720</p>
<button>Toggle</button> 
</body> 


1. Write a jQuery to create fade-in and fade-out effect. 
<!DOCTYPE html> 
<head> 
<title>Basic jQuery</title> 
<script src="jquery-3.6.1.min.js"></script> 
<script> 
$(document).ready(function(){ 
$(".c1").click(function(){ 
$("p").fadeOut(5000); 
}); 
$(".c2").click(function(){  
$("p").fadeIn(5000); 
}) 
}) 
</script> 
</head> 
<body> 
<p>Romal Shah:239720</p> 
<button class="c1">Fade Out</button>
<button class="c2">Fade In</button> 
</body>


1.  Write a jQuery to create fade toggle effect. 
<!DOCTYPE html> 
<head> 
<title>Basic jQuery</title> 
<script src="jquery-3.6.1.min.js"></script> 
<script> 
$(document).ready(function(){ 
$("button").click(function(){ 
$("p").fadeToggle(5000); 
}); 
}) 
</script> 
</head> 
<body> 
<p>Romal Shah:239720</p> 
<button>Fade Toggles</button> 
</body>


1. Write a jQuery to create slide-up and slide-down effect. 
<!DOCTYPE html> 
<head> 
<title>Basic jQuery</title> 
<script src="jquery-3.6.1.min.js"></script> 
<script> 
$(document).ready(function(){ 
$("#b1").click(function(){ 
$("p").slideUp(3000); 
}); 
$("#b2").click(function(){  
$("p").slideDown(3000); 
}) 
}) 
</script> 
</head> 
<body> 
<p>Romal Shah:239720</p> 
<button id="b1">Slide Up</button> 
<button id="b2">Slide Down</button> 
</body>


1. 
Write a jQuery to create slide toggle effect. 
<!DOCTYPE html> 
<head> 
<title>Basic jQuery</title> 
<script src="jquery-3.6.1.min.js"></script> 
<script> 
$(document).ready(function(){ 
$("button").click(function(){ 
$("p").slideToggle(5000); 
}) 
}) 
</script> 
</head> 
<body> 
<p>Romal Shah:239720</p> 
<button>Slide Toggle</button>s 
</body> 

1. 
Write a jQuery to create Mouse Event. 
<!DOCTYPE html> 
<html> 
<head> 
<title>Basic jQuery</title> 
<script src="jquery-3.6.1.min.js"></script> 
<script> 
$(document).ready(function(){ 
$("#p1").mouseleave(function(){ 
alert("Bye! You now leave p1"); 
}) 
}) 
</script> 
</head> 
<body> 
<p id="p1">This is a paragraph</p> 
</body> 
</html>



**Practical 8**
1. 
Practical 8 
Write a jQuery to create animation effect. 
<!DOCTYPE html> 
<head> 
<title>Basic jQuery</title> 
<script src="jquery-3.3.1.min.js"></script> 
<script> 
$(document).ready(function(){ 
$("button").click(function(){ 
$("img").animate({left:50}); 
}) 
}) 
</script> 
<style> 
img{position:relative;} 
</style> 
</head> 
<body> 
<p>Romal:239720</p> 
<img src="Mountain.png" alt="Mountain Image"><br> 
<br><button>Start Animation</button> 
</body>

1. Write a jQuery to animate multiple css properties. 
 
<html> 
<head> 
<script src="jquery-3.6.1.min.js"></script>
<script> 
$(document).ready(function(){ 
    $("#b1").click(function(){ 
        
$("#div1").animate({width:"150px",height:"150px",opacity:"0.5",l
eft:"150"}); 
    }) 
}) 
</script> 
<style> 
#div1{width:100px;height:100px;background:yellow;position:rela
tive;} 
</style> 
</head> 
<body> 
<p> Animation</p> 
<div id="div1"></div> 
<button id="b1">Click to Animate</button> 
</body> 
</html>


1. 
Write a jQuery to perform method of chaining. 
<!DOCTYPE html> 
<head> 
<title>Basic jQuery</title> 
<script src="jquery-3.3.1.min.js"></script> 
<script> 
$(document).ready(function(){ 
$("button").click(function(){ 
$("#p1").css("color","blue").slideUp(2000).slideDown(2000) 
}) 
}) 
</script> 
</head> 
<body> 
<p id="p1">Romal:239720</p> 
<button>Click Me</button> 
</body>


**Practical 9**
1. 
Write a jQuery effect method with a callback function. 
<!DOCTYPE html> 
<head> 
<title>Basic jQuery</title> 
<script src="jquery-3.3.1.min.js"></script> 
<script> 
$(document).ready(function(){ 
$("button").click(function(){ 
$("p").hide("slow",function(){ 
alert("The paragraph is now hidden") 
}) 
}) 
}) 
</script> 
</head> 
<body> 
<p>Romal:239720</p> 
<p>Welcome to MCC</p> 
<button>Click!</button> 
</body>


1. Write a jQuery to get and set text context of the elements. 
 
<!DOCTYPE html> 
<head> 
    <title>Basic jQuery</title> 
    <script src="jquery-3.6.1.min.js"></script> 
    <script> 
        $(document).ready(function(){ 
            $("#b1").click(function(){ 
                var str = $("p").text(); 
    alert(str); 
    }) 
   $("#b2").click(function(){ 
    $("p").text("Hello World"); 
            }) 
        }) 
    </script> 
</head>
<body> 
<p>Romal Shah:239720</p> 
<p> MongoDB</p> 
<button id="b1">Get</button> 
<button id="b2">Set</button> 
</body>

1. 
Write a jQuery to get and set HTML contents of the 
elements. 
<!DOCTYPE html> 
<head> 
<title>Basic jQuery</title>
<script src="jquery-3.6.1.min.js"></script> 
<script> 
$(document).ready(function(){ 
$("#b1").click(function(){ 
var str = $("p").html(); 
alert(str); 
}) 
$("#b2").click(function(){ 
$("p").html("<b>Hello World<b>"); 
}) 
}) 
</script> 
</head> 
<body> 
<p><b>Romal Shah:</b><u>239720</u></p> 
<p> MongoDB</p> 
<button id="b1">Get</button> 
<button id="b2">Set</button> 
</body>

Parsing JSON 
<html> 
<body> 
<script type="text/javascript"> 
var data = '{"name":"Romal","age":20,"dept":"IT"}'; 
var jsonObj = JSON.parse(data, function(name, value) { 
return value; 
});
document.writeln(jsonObj.name); 
for (key in jsonObj) { 
document.writeln("<br/>" + key + " : " + jsonObj[key]); 
} 
var jsonObj = JSON.parse(data, function(name, value) { 
if (name == "sem") { 
return undefined; 
} else { 
return value; 
} 
}); 
for (key in jsonObj) { 
document.writeln("<br/>" + key + " : " + jsonObj[key]); 
} 
</script> 
</body> 
</html> 


3. 
<html> 
<body> 
<script type="text/javascript"> 
var data = '{"name":"Romal","age":20,"dept":"IT"}';
var obj = JSON.parse(data); 
for(var key in obj) 
{ 
document.writeln(“<br/>+”key+":"+obj[key]); 
} 
</script> 
</body> 
</html> 

   
