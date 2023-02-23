# a1cs6235
- **How to setup repo on your machine ?**

	1. git clone https://github.com/ramyakasar/a1cs6235.git
	2. Open project in Eclipse.
	3. Right click on project name and click on build path -> configure build path
	4. In the left panel, click on “java compiler”. Set the compiler compliance level to 1.8
	5. In the left panel, click on “java build path”. Click on Libraries option. There should be 2 entries -Soot jar and JRE system library.

	      a) If the Soot jar entry is “missing”, download the jar separately. Click on “Add external jar” and give the path to the downloaded Soot Jar.

	      b) If the JRE library’s version is not 1.8 , then double click on JRE and click on alternate JRE. Check if JRE 1.8 is present in the drop down list.

		* If present, simply select JRE 1.8.
		* If absent, download JRE 1.8 separately and select “installed JRE”.Click on add libraries and then standard VM. Here give the path to your installed JRE 1.8 . Now again besides alternate JRE, Your new JRE should be visible in the drop down list. 


- **How to get the Control Flow graph of a method ?**

	Your first argument to the internalTransform method is the body of the method. Let’s call it arg0.

	```
	UnitGraph g = new BriefUnitGraph(arg0);
	```

- **You can get Head of Control Flow Graph as follows**

	```
	List<Unit> heads = g.getHeads();
	```

- **You can get successor of a unit as follows** 

	```
	List<Unit> successors = g.getSuccsOf(u); 
	```

- **How to get stmt ?**

	Simply cast the Unit to stmt. 
	Eg: 
		```
		Stmt s = (Stmt) unit;
		```

- **How to get Definition statements ?**
	```
	if(s instanceof DefinitionStmt){

	}
	```

	Once you get the definition statement, you can fetch it's left and right operand as follows :

	```
	DefinitionStmt ds = (DefinitionStmt)s;
	Value leftOp = ds.getLeftOp();
	Value rightOp = ds.getRightOp();
	```

- **How to check if operands are RefLike type ?**
	
	```
	if(leftOp.getType() instanceof RefLikeType){

	}
	```
	
> ***Simple Task to start with : Traverse Control flow graph graph in a control flow order and print the units. (Hint - DFS)***


     
## Instructions for Assignment 1:

Alias Analysis is given below.

http://www.cse.iitm.ac.in/~krishna/cs6235/a1.html

You need to implement the *internalTransform* method in *AliasAnalysis* class under *submit_a1* package.

 *A1* is the main class. It takes the input file from *inputs* folder and queries file from *queries* folder.
 
 ###### Running from command-line:
 java -Dtest.file="queries/Q1.txt" A1 -pp -cp "inputs" -p jb use-original-names:true -app -src-prec java P1
 
- The queries file path is given by -Dtest.file, which can be accessed using System.getProperty("test.file")
- **-pp** : indicates to prepend java class path to soot classpath. Initially soot classpath is empty
- **-cp "inputs"** : indicates to include "inputs"(where P1.java is placed) in soot classpath 
- **-p jb use-original-names:true** : in the jb pack (jimple body), use original names as of source file. This is required to retain the variable names, as our  queries use the java sorce file names . Otherwise, the jimple format will have different variable names.
- **-app** : indicates to run in application mode. Whatever classes referred from argument classes (here P1) will also be application classes(except library classes). Application classes are the ones that will be processed by soot.
- **-src-prec java** : indicates the source precision to be java file instead of .class file. This is to retain original names of variables. If source format is .class, the bytecode variable names will appear in jimple format.

All these options are encoded in the getOptions method of A1 class.

If you want to give any further options or change the existing options, you can try them by passing command line arguments. For normal functioning required for assignment, you need not change any options. 
 
 
      
###### Query form      

Each query is of the form
*&lt;class&gt;:&lt;method&gt;:&lt;var1&gt; alias &lt;var2&gt;*
      
It represents, "Inside class *&lt;class&gt;*, method *&lt;method&gt;*, is *&lt;var1&gt;* alias of *&lt;var2&gt;* at the end of method *&lt;method&gt;*? "
      
Your analysis should answer either "yes" or "No" for this.

The answers should follow the same order as of queries in the query file.
      
Your answers should be present in static String array *answers* in *A1* class which can be accessed as *A1.answers*.

###### Example

Consider the below example,
      
```
class P1 {
  void m1() {
	 A x,y;
	 x = new A();
	 y = new A();
	 x.foo();
	 y.foo();
	 
 }
  void m2() {
	  A a,b,z;
	  boolean c = true;
	  a = new A();
	  b = new A();
	  if(c)
		  z = a;
	  else
		  z = b;
	  z.foo();
 }
}
class A{
	void foo() {
		System.out.println(10);
	}
}
```
      
The Queries
      
```
P1:m1:x alias y


P1:m2:a alias z


P1:m2:a alias b


P1:m2:b alias z
```

should answer
```      
No
Yes
No
Yes
```
It means, A1.answers[0] should contain Yes, A1.answers[1] should contain No, and so on..







