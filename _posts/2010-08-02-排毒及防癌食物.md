---
title: "JADE Tutorial and Primer摘要"
date: 2010-08-02
categories: 
  - "software_programming"
tags: 
  - "jade"
---

JADE Tutorial and Primer 是一个绝好的学习JADE的网站，文章讲解地简单明了，很适合初学者学习。下面是本人在学习过程中根据个人理解的知识摘要。

JADE _Agents_ are defined as subclasses of the predefined class **Agent** and their initial code must be placed in a method called **setup**.

_Agents_ are a bit like Java _Applets_ in that they can't be executed directly; they must execute within a larger program which provides the necessary services. In the case of Applets, a browser or an Applet viewer is needed; for Jade agents the environment is provided by the class **jade.Boot** which finds which Agents to run from command line parameters.

Jade _environments_ are called **containers**. Typically, in a multi-agent application, there will be several containers (with agents) running on different machines. The first container started must be a **main** container which maintains a central registry of all the others so that agents can discover and interact with each other.

Agent actions are normally specified through **Behaviour** classes. More exactly, the actions are described in the "**action**" method of these Behaviours. The setup method only serves to create instances of these behaviours and linking them to the Agent object.

A last point is the provision of a mechanism to terminate the behaviour. In Jade, as long as a behaviour is not "**done**", its action method will be called repeatedly after every **event** - such as receipt of a message or expiry of a timer delay.

Agent Parameters: the parameters are placed in a list seperated by spaces after the "name:class" agent specifier. For example: fred:ParamAgent(3 "Hi there"). In Jade, the arguments are obtained by calling the method _getArguments_ which returns an array of **Objects** which must be cast to Strings Reversing single and double quotes can give surprising results.

为了实现Agent的并行，可以借助Java的线程机制。但是Java的线程不适合大规模的并行。所以，jade使用behaviour实现并行。

A behaviour is basically an _Event Handler_, a method which describes how an agent reacts to an _event_.  In Jade, Behaviours are classes and the _Event Handler_ code is placed in a method called **action**.

In JADE, messages adhere strictly to the ACL (Agent Communication Language) standard which allows several possibilities for the encoding of the actual _content_. In particular, Jade supports FIPA's SL (Semantic Language), a LISP-like encoding of _concepts_, _actions_ and_predicates_. It also allows the content to be serialized Java objects.

Our message uses the most common _performative_: INFORM whereby one agent gives another some useful information. Other types are: QUERY to ask a question, REQUEST to ask the other to do something and PROPOSE to start bargaining. Performatives for answers include AGREE or REFUSE.

We use **_add_**_Receiver_ because there is no **_set_**_Receiver_ method.

Note that, if you don't call _block()_, your behaviour will stay active and cause a **LOOP**. Generally all action methods should end with a call to _block()_ or invoke it before doing _return_.

the **CyclicBehaviour**, which stays active as long as its agent is alive. by using **CyclicBehaviour**, we don't need to specify _done_.

To simplify answering, Jade provides a method _createReply()_ which creates a new message with the sender and receiver attributes switched and all other attributes set correctly. Generally, only the content and performative have to be modified before sending it back.

For agents to interact usefully in open systems, it is imperative that they use the same language conventions and the same vocabulary. The DF entries thus concentrate on listing the **ontologies**, **protocols** and **languages** which are supported by the agents. Additionally, entries have sets of **services** which are characterized by aname and _name-value_ properties as well as the ontology/language/protocol conventions they support

Each agent is allowed only ONE entry in the DF. Attempts to register an agent already in the DF gives an Exception.

the WakerBehaviour，its delay is computed from the time the behaviour is**created**.

一定要区别好Behavours Created和Started.

The key to implementation of interaction protocols is to assign to each conversation a unique identifier, the conversationID (CID).
