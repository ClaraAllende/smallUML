

#SmallUML


#An UML diagram modeling tool written in Pharo Smalltalk



##1\. \(Not\) Yet Another UML diagram dsl
SmallUML is a DSL written in Pharo Smalltalk to help you create cool documentation for your system\. 
Some of its goodies are: 


-  Open a Diagram Browser for visualizing the existing diagrams
-  Create and edit diagrams programatically describing them with "diagram code" \(a protocol of methods meant to describe diagrams\)
-  Every diagram you build through the Diagram Browser it's saved as "diagram code", so you can share it as code that will reproduce your diagram :\) That means that diagrams can 'travel' along it's package when you commit your changes with Monticello\! And then they can be edited by anybody, they're not just a pretty picture\.
-  You can export your diagram as a PNG picture or you can export it's "diagram code" as a workspace\.
-  Class Diagrams and Object Diagrams can be created using SmallUML \(more to come\)




##2\.  How does it work?
In SmallUML all the diagrams can be seen as nodes and connectors, each one of them having their own type, depending on the diagram\. For example, for class diagrams nodes are "boxes" \(class boxes, interface boxes, trait boxes, etc\) and the connectors are associations \(composition, hierarchy, uses, etc\); for object diagrams nodes are circles \(objects, collections, etc\), and the connectors are composition associations between the objects\.

SmallUML doesn't generate diagrams automatically \(not yet\), but instead relies on the developer/documenter\(?\) knowledge of *which parts* of the system need to be communicated\.

For creating a class diagram, just evaluate in a workspace:


```smalltalk
DiagramsHolder openDiagramBrowser .
```



You will see all the available diagrams\. Right click on any of them, select *Add diagram*, and provide a name\.
Then if you browse `DiagramHolder` class, you will find a method with the name you have provided, in which you can define the nodes and relations:
<a name=""></a><figure><img src="figures/diagramsHolder.png" width="60%"></img><figcaption>Figure 1: DiagramsHolder</figcaption></figure>

So for example, the following code snippet


```smalltalk
pirates
	| d pirate byteSymbol treasureQuest mission ship |
	pirate := ClassBox named: 'Pirate'.
	pirate instanceVariables: #('alcoholLevel').
	pirate instanceMethods: #(#alcoholLevel: #items: #isUsefulForTheMission: #isDrunkEnough #includesItem:).	"Positioning"
	pirate position: 663.0 @ 201.0.
	byteSymbol := ClassBox named: 'ByteSymbol'.	"Positioning"
	byteSymbol position: 951.0 @ 253.0.
	treasureQuest := ClassBox named: 'TreasureQuest'.
	treasureQuest instanceMethods: #(#canUsePirate:).	"Positioning"
	treasureQuest position: 50.0 @ 240.0.
	mission := ClassBox named: 'Mission'.
	mission instanceMethods: #(#canUsePirate:).	"Positioning"
	mission position: 57.0 @ 26.0.
	ship := ClassBox named: 'Ship'.
	ship instanceMethods: #(#mission: #acceptIntoTripulation:).	"Positioning"
	ship position: 318.0 @ 232.0.	"Relationships"
	pirate hasLotsOf: byteSymbol labeledAs: 'items'.	"Relationships"
	treasureQuest inheritsFromClass: mission.	"Relationships"
	ship hasA: treasureQuest labeledAs: 'mission'.
	ship hasLotsOf: pirate labeledAs: 'tripulation'.
	d := (ClassDiagram new name: 'Pirates!')
		addDiagramNode: pirate;
		addDiagramNode: byteSymbol;
		addDiagramNode: treasureQuest;
		addDiagramNode: mission;
		addDiagramNode: ship.
	^ d
```



generates this diagram:
<a name=""></a><figure><img src="figures/pirates.png" width="90%"></img><figcaption> Figure 2: A smallUML class diagram</figcaption></figure>



##3\. How do I get SmallUML in my image?

Simple: just copy the following script in a workspace:


```smalltalk
Gofer it
		smalltalkhubUser: 'Uqbar' project: 'SmallUml';
		configurationOf: 'SmallUML';
		loadVersion: #stable .
```



*Et voila\!* ready to use :\)



##4\.  Doubts? Complaints? Suggestions? 

SmallUML is a work in progress, and the most important thing to keep on improving it is your collaboration\.
So, if you have doubts, suggestions, feature requests or bug reports, please fill them in at the [issue tracker](https://github.com/ClaraAllende/smallUML/issues)\.



##5\.  To come:
&nbsp;

-  Screencast on how to create and customize diagrams
-  Improve class diagrams
-  Sequence diagrams

