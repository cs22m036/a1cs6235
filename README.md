# a1cs6235
**How to setup repo on your machine ?**

1. git clone https://github.com/ramyakasar/a1cs6235.git
2. Open project in Eclipse.
3. Right click on project name and click on build path -> configure build path
4. In the left panel, click on “java compiler”. Set the compiler compliance level to 1.8
5. In the left panel, click on “java build path”. Click on Libraries option. There should be 2 entries -Soot jar and JRE system library.

      a) If the Soot jar entry is “missing”, download the jar separately. Click on “Add external jar” and give the path to the downloaded Soot Jar.
      
      b) If the JRE library’s version is not 1.8 , then double click on JRE and click on alternate JRE. Check if JRE 1.8 is present in the drop down list.
      
        i. If present, simply select JRE 1.8.
        ii. If absent, download JRE 1.8 separately and select “installed JRE”.Click on add libraries and then standard VM. Here give the path to your installed JRE 1.8 . Now again besides alternate JRE, Your new JRE should be visible in the drop down list. 


**How to get the Control Flow graph of a method ?**

Your first argument to the internalTransform method is the body of the method. Let’s call it arg0.

UnitGraph g = new BriefUnitGraph(arg0);

**You can get Head of Control Flow Graph as follows**

List<Unit> heads = g.getHeads();

**You can get successor of a unit as follows** 

List<Unit> successors = g.getSuccsOf(u); 

**Your task is to traverse Control flow graph graph in a control flow order and print the units. (Hint - DFS) . Try to implement this by monday.**
