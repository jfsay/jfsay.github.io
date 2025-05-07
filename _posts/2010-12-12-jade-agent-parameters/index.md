---
title: "JADE Agent Parameters"
date: 2010-12-12
categories: 
  - "software_programming"
tags: 
  - "jade"
---

**Agent Parameters**

It is often useful to be able to pass parameters to agents. This is described in the Jade Programming Tutorial (sect. 3.4). On a command line, the parameters are placed in a list seperated by spaces after the "name:class" agent specifier. For example:

% java jade.Boot fred:ParamAgent(3 "Hi there")

Here fred will be passed 2 parameters: an integer and a string. In standard Java, we are used to retrieving command arguments from a _String array_ parameter to the static method **main**. With JADE, retrieving arguments is a bit different because the same mechanism is used both to pass arguments from a command line and to pass arguments to agents created by programming.

In Jade, the arguments are obtained by calling the method _getArguments_ which returns an array of **Objects** which must be cast to Strings (in this case). Here is an example of a ParamAgent which can retrieve the arguments "3" and "Hi there" shown above.

```
/**************************************************************   
     ParamAgent.java:  Retrieving parameters
 **************************************************************/   
     
     import jade.core.Agent;
    
     public class ParamAgent extends Agent 
     { 
        protected void setup() 
        { 
            Object[] args = getArguments();
            String s;
            if (args != null) {
                for (int i = 0; i<args.length; i++)="" {="" s="(String)" args[i];="" system.out.println("p"="" +="" i="" ":="" "="" s);="" }="" extracting="" the="" integer.="" int="" (string)="" args[0]="" );="" system.out.println("i*i=" + i*i);
            }
        }
     }
```

The command line shown above doesn't work under **UNIX** or **Mac OSX.**

jean% java jade.Boot fred:ParamAgent(1 " hi="" there")<="" p="">

_tcsh: Badly placed ()'s._

With these systems, each agent specifier (name, class & argument list) must be **quoted**.

% java jade.Boot 'fred:ParamAgent(3 "fred toto")'

p0: 3

p1: fred toto

i\*i= 9

Reversing single and double quotes can give surprising results; in this case: 3 arguments !!!

jean% java jade.Boot "fred:ParamAgent(3 'fred toto')"

p0: 3

p1: 'fred

p2: toto'

i\*i= 9

**Passing arguments to newly created Agents**

Similarly, an array of arguments can be provided for new agents in the third parameter of _createNewAgent_. Here is how we could create a ParamAgent with the same name and arguments as in our earlier example. Note that the arguments are passed as _Objects_; thus, simple types must be converted to Strings or Wrapper classes.

```
Object [] args = new Object[2];
args[0] = "3";
args[1] = "Allo there";
	 
String name = "Fred" ;
AgentContainer c = getContainerController();
try {
       AgentController a = c.createNewAgent( name, "ParamAgent", args );
       a.start();
     }
catch (Exception e){}

```

**Responder Agent**

```
// ------------------------------------------------------------
//   ParamAgent:   An Agent receiving parameters             
//
//   Usage:    % javac ParamAgent.java
//             % java jade.Boot  fred:ParamAgent(3 "Allo there")
//
// ... on UNIX, the agent specifier and arguments must be quoted:
//
//             % java jade.Boot 'fred:ParamAgent(3 "Allo there")'
// ------------------------------------------------------------

 import jade.core.Agent;

 public class ParamAgent extends Agent 
 { 
	protected void setup() 
	{ 
		Object[] args = getArguments();
		String s;
		if (args != null) {
			for (int i = 0; i<args.length; i++)="" {="" s="(String)" args[i];="" system.out.println("p"="" +="" i="" ":="" "="" s);="" }="" int="" (string)="" args[0]="" );="" args[1];="" system.out.println("i*i=" + i*i);
			System.exit(1);
		}
	}
 }
```

**Reference:**

- http://www.iro.umontreal.ca/~vaucher/Agents/Jade/primer2.html

- http://www.iro.umontreal.ca/~vaucher/Agents/Jade/primer4.html

- http://www.iro.umontreal.ca/~vaucher/Agents/Jade/code/ch\_2/ParamAgent.java
