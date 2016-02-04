<img src="img/Logo_b.png" alt="JooMDDLogo" height="300" style="max-width:100%;float:right;">

**JooMDD** provides a set of plugins for a model-driven development of Joomla! extension 
packages. 
The current version of JooMDD can be used within ***Eclipse***, 
***IntelliJ IDEA***, ***PHPStorm***, and ***Orion***.

***
## Installation of JooMDD ##
Please follow this installation guide to use JooMDD within Eclipse, IntelliJ, PHPStorm, and Orion. 

**Attention:** The support of PHPStorm is currently experimental. Therefore some effort is needed during the installation
### Eclipse ###
Install the JooMDD tools through the use of the following update site within the Eclipse update manager. Supported versions are:
*Kepler*, *Luna*, and *Mars*.

#### JooMDD update site (Eclipse): <http://icampus.thm.de/JooMDDUpdateSite_Eclipse> ####
### IntelliJ IDEA ###
Install the JooMDD tools through the use of the following update site within IntelliJ's plugin manager. The currently supported 
(tested)version is IntelliJ IDEA 15. Please feel free to try JooMDD within other IntelliJ versions.
#### Precondition: ####
Install Xtext IDEA Core from the repositories of IntelliJ. (In IntelliJ go to: File/Settings/Plugins/Browse Repositories search: "Xtext Idea Core" and install the plugin)

#### JooMDD update site (IntelliJ IDEA): <http://icampus.thm.de/JooMDDUpdateSite_IntelliJ> ####

### PHPStorm ###
Due to the fact, that the PHPStorm support is in a kind of beta state, you need some more effort for the installation. But don't 
be scared, it's just copy&paste of some files ;-). Please ensure, that you have the latest version of PHPStorm installed. We tested 
the following instructions with version 10.0.3.
#### Precondition: ####
PHPStorm 10.0.3, Download of some files (includes configurated Xtext and the EJSL language) here: ...

#### Prepare PHPStorm (only first time): ####
*	Copy IntelliJdepencies.jar into path: PHPStorm installation\lib\  .
*	Now install the two downloaded plugins (Xtext and EJSL) via "Install plugin from disk ..." (Menu: File/Settings/Plugins/).

#### Add the language to your Project: ####

### Orion ###

***
## Getting Started ##
### The eJSL language###
 <img src="img/eJSL_Logo_trans.png" alt="eJSLLogo" height="200" style="max-width:100%;float:right;">
 
The **eJSL** plugin can be used to create extensions for the Joomla CMS in a model-driven way. 
Through the creation of eJSL-specific models a tremendous amount of code becomes generated automatically. 
eJSL supports the definition of several Joomla extension types like components, modules, plugins, and 
libraries. The generated code can be used within web pages, running on [Joomla 3.x](https://www.joomla.org/3). 

Please make sure, that you've installed the eJSL part of JooMDD to follow the next steps.
### 1. Create a new eJSL project ###
There are two ways to create an eJSL project:

#### Manual project creation: ####
1. Create a new project of any type (e.g. a general, Java, or PHP project)
2. Create a new file of any name with the ending .eJSL (e.g. *model.eJSL*)
3. Start creating your model containing entities, pages, and extensions

#### Using the eJSL Project Wizard: ####

##### Eclipse #####
Instead of creating an eJSL project manually, you can get started easier, using the eJSL project wizard. 
For this, create a new project and within the "new Project" dialogue open the folder Xtext. Within this 
folder you should see *"EJSL Project"*. Through a double-click on this project type, the required project 
structure becomes generated containing source folders for your models (*src*) and for the code generated 
based on your models (*src-gen*). In addition, an example model is created within the src folder which 
can be used for a straightforward introduction.

##### IntelliJ and PHPStorm #####
##### Orion #####

### 2. Create a model ###
eJSL allows you the definition of different parts of a Joomla extension. Starting with the definition 
of a data structure (***entities***) on to its presentation (***pages***) up to the specification of 
Joomla-specific ***extensions***.

### 3. Code generation ###
When you save your model, the code generator creates your modelled Joomla extensions within the project's 
src-gen folder. The extensions are installable within Joomla 3 web sites and don't need any additional 
line of code. However, if you knwo what you do, you can extend the generated code through individual features. 
But beware: All the code within the src-gen folder becomes COMPLETELY overwritten, when you change your model 
and save it. Therefore we recommend to copy generated extensions to another folder within your project, where 
you can extend them without loosing them after a new code generation. Another and cleaner option is using a 
versioning tool like git to store your individual added code.

***
## Copyright ##
Copyright (C) 2013 - 2016, [iCampus](http://icampus.thm.de) - [Technische Hochschule Mittelhessen](http://www.thm.de). 
All rights reserved.
This project is distributed under the GPL (GNU General Public License) version 2. For further information see 
the [License details](https://git.thm.de/JooMDD/joomdd_repo/blob/master/LICENSE).

***
Please feel free to [contact](icampu@lists.thm.de) us, if you find some bugs or if you like to contribute to the project.