Download Link: https://assignmentchef.com/product/solved-cst-8219-assignment-2
<br>
Vector Graphic with Overloaded Operators

<strong>Purpose: </strong>This assignment is a direct continuation of assignment 1 that uses overloaded operators. In anticipation of polymorphism in ass3 it now stores Graphic Elements as a dynamic array. Also the Stash is replaced by a better container: the vector template class.

Part of the code is shown on the next page; it is also on the Web Site in text files that you can copy and paste from so you don’t make any mistakes. You must use this code without modification or additions because I will use it to mark your assignment. Your task is to implement the member functions that are declared in the Point.h, Line.h, GraphicElement.h and VectorGraphic.h header files and not add any new ones – your code is in the files Point.cpp, Line.cpp, GraphicElement.cpp and VectorGraphic.cpp.




In this assignment, when the application is running the user can

<ul>

 <li>Add a new Graphic Element (together with its lines) to the Vector Graphic</li>

 <li>Delete a Graphic Element</li>

 <li>Report a Graphic Element</li>

 <li>Print all the details of the Graphic Elements in the Vector Graphic</li>

 <li>Edit a Graphic Element</li>

</ul>




<strong>An example of the output of the running application is given at the end. Yours must work identically and produce identical output. </strong>




Note the following:

<ul>

 <li>The files you submit must be named Point.cpp, Line.cpp, GraphicElement.cpp and VectorGraphic.cpp.</li>

 <li>you must use C++ syntax including new and delete and cin and cout</li>

 <li>You can only use functions like strlen() and strcpy() or similar etc. from the standard C library to handle strings (this assignment does not use the C++ string class).</li>

 <li>When the application terminates it releases <strong><u>all</u></strong> dynamically allocated memory so it does not have a resource leak (or you lose 30%).</li>

</ul>

See the Marking Sheet for how you can lose marks, but you will lose at least 60% if: you change or add to the supplied code, it fails to build in Visual Studio 2013, it crashes in normal operation (such as printing from an empty list etc.), it doesn’t produce the example output.

Part of the code is shown on the next page. You MUST use this code <strong>without modification.</strong> Your task is to add the implementation of the functions that are declared using the style of the posted Submission Standard. All your code is in the files Point.cpp, Line.cpp, GraphicElement.cpp and VectorGraphic.cpp.

<strong> </strong>

<strong><u>What to Submit :</u></strong> Use Blackboard to submit this assignment as a zip file (<strong>not </strong>RAR) containing only the source code files (Point.cpp, Line.cpp, GraphicElement.cpp and VectorGraphic.cpp). The name of the zipped folder <strong><u>must </u></strong>contain your name as a prefix so that I can identify it, for example using my name the file would be tyleraAss2CST8219.zip. It is also vital that you include the Cover Information (as specified in the Submission Standard) as a file header in your source file so the file can be identified as yours. Use comment lines in the file to include the header.

Before you submit the code,

<ul>

 <li>check that it builds and executes in Visual Studio 2013 as you expect – if it doesn’t build for me, for whatever reason, you get a deduction of at least 60%.</li>

 <li>make sure you have submitted the correct file – if I cannot build it because the file is wrong or missing from the zip, even if it’s an honest mistake, you get 0.</li>

 <li>there’s a late penalty of 25% per day. Don’t send me file(s) as an email attachment – it will get 0.</li>

</ul>




<strong><em>Example code – I will use it to mark your assignment. Don’t change or add to it. </em></strong>

<table width="623">

 <tbody>

  <tr>

   <td width="312">// Point.h#ifndef POINT#define POINT class Point{int x, y; public:Point() :x(0), y(0){}Point(int x, int y) :x(x), y(y){}friend ostream&amp; operator&lt;&lt;(ostream&amp;,Point&amp;);}; #endif</td>

   <td width="311">// Line.h#ifndef LINE#define LINE class Line{Point start;            Point end; public:Line() :start(), end(){}Line(Point start, Point end) :start(start), end(end){}friend ostream&amp; operator&lt;&lt;(ostream&amp;, Line&amp;);}; #endif</td>

  </tr>

 </tbody>

</table>

<strong> </strong>

<table width="623">

 <tbody>

  <tr>

   <td width="55">// GraphicElement.h {public:            GraphicElement&amp;);}; #endif</td>

   <td width="251">#ifndef GRAPHICELEMENT #define GRAPHICELEMENTclass GraphicElementchar* name; vector&lt;Line&gt; Lines; // a vectorof LinesGraphicElement():name(nullptr){};GraphicElement(char*);GraphicElement(vector&lt;Line&gt;, char*);GraphicElement(GraphicElement&amp;);~GraphicElement(){if (name)                      delete []name;}GraphicElement&amp; operator=(GraphicElement&amp;); friend ostream&amp; operator&lt;&lt;(ostream&amp;,</td>

   <td width="55">// VectorGraphic.hclass VectorGraphic{   public:             }; #endif</td>

   <td width="262">#ifndef VECTORGRAPHIC#define VECTORGRAPHIC GraphicElement** Elements;    // elements on the heap unsigned int numElements;     // how manyVectorGraphic():numElements(0),Elements(nullptr){}~VectorGraphic(){for (int i = 0; i &lt; numElements; i++)delete Elements[i];            delete[] Elements;}void AddGraphicElement(); void DeleteGraphicElement(); void ReportVectorGraphic(); void EditGraphicElement(); GraphicElement&amp; operator[](int); friend ostream&amp; operator&lt;&lt;(ostream&amp;, VectorGraphic&amp;);</td>

  </tr>

 </tbody>

</table>




<table width="623">

 <tbody>

  <tr>

   <td colspan="3" width="623">// ass2 W17 #define _CRT_SECURE_NO_WARNINGS#define _CRTDBG_MAP_ALLOC      // need this to get the line identification//_CrtSetDbgFlag(_CRTDBG_ALLOC_MEM_DF|_CRTDBG_LEAK_CHECK_DF); // in main, after local declarations//NB must be in debug build#include &lt;crtdbg.h&gt; #include &lt;iostream&gt; #include &lt;vector&gt; using namespace std; #include “Point.h”#include “Line.h”#include “GraphicElement.h” #include “VectorGraphic.h” enum{ RUNNING = 1 }; VectorGraphic Image; int main(){char response;_CrtSetDbgFlag(_CRTDBG_ALLOC_MEM_DF | _CRTDBG_LEAK_CHECK_DF); while (RUNNING){cout&lt;&lt;endl&lt;&lt;“Please select an option:
”&lt;&lt;endl;                                cout&lt;&lt;“1. Add a Graphic Element
”;                          cout&lt;&lt;“2. Delete a Graphic Element
”;                                 cout&lt;&lt;“3. Report a Graphic Element
”;                                 cout&lt;&lt;“4. List the Graphic Elements
”;cout&lt;&lt;“5. Edit a Graphic Elements
”;                                cout&lt;&lt;“q. Quit
”;                                 cout&lt;&lt;“CHOICE: “;cin&gt;&gt;response; switch (response){case ‘1’:Image.AddGraphicElement(); break;case ‘2’:Image.DeleteGraphicElement(); break;                          case ‘3’:</td>

  </tr>

  <tr>

   <td width="103">           </td>

   <td width="48">           </td>

   <td width="472">          int index;cout &lt;&lt; “Please enter the index of the Graphic Element: “;            cin &gt;&gt; index;       cout &lt;&lt; Image[index];break;case ‘4’:Image.ReportVectorGraphic(); break; case ‘5’:Image.EditGraphicElement(); break; case ‘q’:return 0; default:cout&lt;&lt;“Please enter a valid option
”;} cout&lt;&lt;endl;</td>

  </tr>

  <tr>

   <td width="103">  }</td>

   <td colspan="2" width="520">} return 0;</td>

  </tr>

 </tbody>

</table>




Example Output:







Please select an option:




<ol>

 <li>Add a Graphic Element</li>

 <li>Delete a Graphic Element</li>

 <li>Report a Graphic Element</li>

 <li>List the Graphic Elements 5. Edit a Graphic Elements</li>

 <li>Quit</li>

</ol>

CHOICE: 1

Please enter the name of the new GraphicElement(&lt;256 characters): big mouth

How many lines are there in the new GraphicElement? 4

<a href="#_Toc11366">Please enter the x coord of the start point of line index 0 1 Please enter the y coord of the start point of line index 0                                                                                             2 </a>

<a href="#_Toc11367">Please enter the x coord of the end point of line index 0                                                                     3 </a>

<a href="#_Toc11368">Please enter the y coord of the end point of line index 0                                                                     4 </a>




Please enter the x coord of the start point of line index 1 5

Please enter the y coord of the start point of line index 1 6

Please enter the x coord of the end point of line index 1 7

Please enter the y coord of the end point of line index 1 8

Please enter the x coord of the start point of line index 2 9

Please enter the y coord of the start point of line index 2 0

Please enter the x coord of the end point of line index 2 1

Please enter the y coord of the end point of line index 2 2

Please enter the x coord of the start point of line index 3 3

Please enter the y coord of the start point of line index 3 4

Please enter the x coord of the end point of line index 3 5

Please enter the y coord of the end point of line index 3 6







Please select an option:

<ol>

 <li>Add a Graphic Element</li>

 <li>Delete a Graphic Element</li>

 <li>Report a Graphic Element</li>

 <li>List the Graphic Elements 5. Edit a Graphic Elements</li>

 <li>Quit</li>

</ol>

CHOICE: 1

Please enter the name of the new GraphicElement(&lt;256 characters): left eye

How many lines are there in the new GraphicElement? 3

Please enter the x coord of the start point of line index 0 1

Please enter the y coord of the start point of line index 0 2

<h1><a name="_Toc11367"></a>Please enter the x coord of the end point of line index 0 3</h1>

<h1><a name="_Toc11368"></a>Please enter the y coord of the end point of line index 0 4</h1>

Please enter the x coord of the start point of line index 1 5

Please enter the y coord of the start point of line index 1 6

Please enter the x coord of the end point of line index 1 7

Please enter the y coord of the end point of line index 1 8

Please enter the x coord of the start point of line index 2 9

Please enter the y coord of the start point of line index 2 0

Please enter the x coord of the end point of line index 2 1

Please enter the y coord of the end point of line index 2 2







Please select an option:

<ol>

 <li>Add a Graphic Element</li>

 <li>Delete a Graphic Element</li>

 <li>Report a Graphic Element</li>

 <li>List the Graphic Elements 5. Edit a Graphic Elements</li>

 <li>Quit</li>

</ol>

CHOICE: 4

VectorGraphic Report




Reporting Graphic Element #0 name = big mouth

Line #0: start is x = 1, y = 2. end is x = 3, y = 4

Line #1: start is x = 5, y = 6. end is x = 7, y = 8

Line #2: start is x = 9, y = 0. end is x = 1, y = 2

Line #3: start is x = 3, y = 4. end is x = 5, y = 6




Reporting Graphic Element #1 name = left eye

Line #0: start is x = 1, y = 2. end is x = 3, y = 4

Line #1: start is x = 5, y = 6. end is x = 7, y = 8

Line #2: start is x = 9, y = 0. end is x = 1, y = 2







Please select an option:

<ol>

 <li>Add a Graphic Element</li>

 <li>Delete a Graphic Element</li>

 <li>Report a Graphic Element</li>

 <li>List the Graphic Elements 5. Edit a Graphic Elements</li>

 <li>Quit</li>

</ol>

CHOICE: 3

Please enter the index of the Graphic Element: 1 name = left eye

Line #0: start is x = 1, y = 2. end is x = 3, y = 4

Line #1: start is x = 5, y = 6. end is x = 7, y = 8

Line #2: start is x = 9, y = 0. end is x = 1, y = 2







Please select an option:

<ol>

 <li>Add a Graphic Element</li>

 <li>Delete a Graphic Element</li>

 <li>Report a Graphic Element</li>

 <li>List the Graphic Elements 5. Edit a Graphic Elements</li>

 <li>Quit</li>

</ol>

CHOICE: 2

Please enter the index for the element to delete, between 0 and 1 0







Please select an option:

<ol>

 <li>Add a Graphic Element</li>

 <li>Delete a Graphic Element</li>

 <li>Report a Graphic Element</li>

 <li>List the Graphic Elements 5. Edit a Graphic Elements</li>

 <li>Quit</li>

</ol>

CHOICE: 4

VectorGraphic Report




Reporting Graphic Element #0 name = left eye

Line #0: start is x = 1, y = 2. end is x = 3, y = 4

Line #1: start is x = 5, y = 6. end is x = 7, y = 8

Line #2: start is x = 9, y = 0. end is x = 1, y = 2







Please select an option:




<ol>

 <li>Add a Graphic Element</li>

 <li>Delete a Graphic Element</li>

 <li>Report a Graphic Element</li>

 <li>List the Graphic Elements 5. Edit a Graphic Elements</li>

 <li>Quit</li>

</ol>

CHOICE: 5

EDIT A GRAPHIC ELEMENT

Please enter the index for the element to edit, between 0 and 0 0

Please enter the new name of the GraphicElement(&lt;256 characters): right eye

How many lines are there in the GraphicElement? 1

Please enter the x coord of the start point of line index 0 1

Please enter the y coord of the start point of line index 0 2

Please enter the x coord of the end point of line index 0 3 Please enter the y coord of the end point of line index 0 4







Please select an option:




<ol>

 <li>Add a Graphic Element</li>

 <li>Delete a Graphic Element</li>

 <li>Report a Graphic Element</li>

 <li>List the Graphic Elements 5. Edit a Graphic Elements</li>

 <li>Quit</li>

</ol>

CHOICE: 4

VectorGraphic Report




Reporting Graphic Element #0 name = right eye

Line #0: start is x = 1, y = 2. end is x = 3, y = 4







Please select an option:

<ol>

 <li>Add a Graphic Element</li>

 <li>Delete a Graphic Element</li>

 <li>Report a Graphic Element</li>

 <li>List the Graphic Elements 5. Edit a Graphic Elements</li>

 <li>Quit CHOICE:</li>

</ol>