<img src="img/Logo_b.png" alt="JooMDDLogo" height="300" style="max-width:100%;float:right;">

**JooMDD** provides a set of plugins for a model-driven development of Joomla! extension 
packages. 
The current version of JooMDD can be used within ***Eclipse***, 
***IntelliJ IDEA***, and ***PhpStorm***.

In addition, we provide **jext2eJSL** to create eJSL-based models based on existing Joomla 3.x extension packages.
We are currently working on the documentation of jext2eJSL. If you are interested in using the tool, see the current (german) 
documentation [here](https://wiki.thm.de/Reverse-Engineering_(Joomla-Code_zu_eJSL-Instanzmodell)).

***
## Installation of JooMDD ##
Please follow this installation guide to use JooMDD within Eclipse, IntelliJ, and PhpStorm. 

**Attention:** The support of PhpStorm is currently experimental. Therefore some effort is needed during the installation
### Eclipse ###
Install the JooMDD tools through the use of the following update site within the Eclipse update manager. Supported versions are:
*Kepler*, *Luna*, and *Mars*.

#### JooMDD update site (Eclipse): <https://raw.githubusercontent.com/icampus/JooMDD/master/Eclipse/JooMDDUpdateSite/site.xml> ####
### IntelliJ IDEA ###
Install the JooMDD tools through the use of the following update site within IntelliJ's plugin manager. The currently supported 
(tested)version is IntelliJ IDEA 15 and 2016. Please feel free to try JooMDD within other IntelliJ versions.
#### Precondition: ####
**Step 1**: Install Xtext IDEA Core (org.eclipse.xtext.idea-2.9.2) from the repositories of IntelliJ. (In IntelliJ go to: File/Settings/Plugins/Browse Repositories search: "Xtext Idea Core" and install the plugin).
*Alternatively* you can download the raw zip file (org.eclipse.xtext.idea-2.9.2.zip) which can be found in the IntelliJ folder within this repository.

**Step 2:** Install the eJSL Plugin via the repositories manager using the following IntelliJ IDEA update site.

#### JooMDD update site (IntelliJ IDEA): <https://raw.githubusercontent.com/icampus/JooMDD/master/IntelliJ/ideaRepository/updatePlugins.xml> ####

*Alternatively* you can download the plugins from this repository and install them manually into your IDE.

### PhpStorm ###
Due to the fact, that the PhpStorm support is in a kind of beta state, you need some more effort for the installation. But don't 
be scared, it's just copy&paste of some files ;-). Please ensure, that you have the latest version of PhpStorm installed. We tested 
the following instructions with version 10.0.3 and 2016.1.
#### Precondition: ####
**Step 1:** Download and install Xtext IDEA Core (org.eclipse.xtext.idea-2.9.2.zip) from this repository via PhpStorm (File->Settings->Plugins).

**Step2:** Download IntelliJdepencies10.0.3.jar (PhpStorm 10) or IntelliJdependencies2016.x.jar (PhpStorm2016) and copy it into the lib path of your PhpStorm installation (^PhpStorm installation^\lib\ ). This must be done only once.

**Step 3:** Install the eJSL Plugin via the repositories manager using the following PhpStorm update site.

#### JooMDD update site (PhpStorm): <https://raw.githubusercontent.com/icampus/JooMDD/master/PHPStorm/ideaRepository/updatePlugins.xml> ####

*Alternatively* you can download the plugins from this repository and install them manually into your IDE.

***
## Getting Started ##
### The eJSL language###
 <img src="img/eJSL_Logo_trans.png" alt="eJSLLogo" height="100" style="max-width:100%;float:right;">
 
The **eJSL** plugin can be used to create extensions for the Joomla CMS in a model-driven way. 
Through the creation of eJSL-specific models a tremendous amount of code becomes generated automatically. 
eJSL supports the definition of several Joomla extension types like components, modules, plugins, and 
libraries. The generated code can be used within web pages, running on [Joomla 3.x](https://www.joomla.org/3). 

Please make sure, that you've installed the eJSL part of JooMDD to follow the next steps.
### 1. Create a new eJSL project ###
There are two ways to create an eJSL project:

#### Manual project creation (works for Eclipse, IntelliJ IDEA, and PhpStorm): ####
1. Create a new project of any type (e.g. a general, Java, or PHP project)
2. Create a new file of any name with the ending .eJSL (e.g. *model.eJSL*)
3. Start creating your model containing entities, pages, and extensions

#### Using the eJSL Project Wizard: ####
Instead of creating an eJSL project manually, you can get started easier, using the eJSL project wizard. 

##### Eclipse #####
Create a new project and within the "new Project" dialogue open the folder eJSL Wizard. 

<img src="img/eclipse_pw_1.png" alt="Eclipse Project Wizard" height="300" style="max-width:100%;float:right;">
<img src="img/eclipse_pw_2.png" alt="Eclipse Project Wizard 2" height="300" style="max-width:100%;float:right;">
<img src="img/eclipse_pw_3.png" alt="Eclipse Project Wizard 3" height="300" style="max-width:100%;float:right;">

Within this folder you should see *"EJSL Project"*. Give your project a name and select a model example template.
Through a click on the Finish-Button the required project structure becomes generated containing source folders 
for your models (*src*) and for the code generated based on your models (*src-gen*). The chosen example model 
is created within the src folder which can be used for a straightforward introduction.

<img src="img/eclipse_pw_4.png" alt="Eclipse Project Wizard 4" height="300" style="max-width:100%;float:right;">

##### IntelliJ #####
Create a new project and within the "new Project" dialogue click on the *eJSL* section. 

<img src="img/ij_pw_1.png" alt="IntelliJ IDEA Project Wizard" height="300" style="max-width:100%;float:right;">
<img src="img/ij_pw_2.png" alt="IntelliJ IDEA Project Wizard 2" height="300" style="max-width:100%;float:right;">

Select a model example template and subsequently give you project a name.
Through a click on the Finish-Button the required project structure becomes generated containing source folders 
for your models (*src*) and for the code generated based on your models (*src-gen*). The chosen example model 
is created within the src folder which can be used for a straightforward introduction.

<img src="img/ij_pw_3.png" alt="IntelliJ IDEA Wizard 3" height="300" style="max-width:100%;float:right;">

##### PhpStorm #####
Create a new project and within the "new Project" dialogue click on the *eJSL* section.

<img src="img/php_pw_1.png" alt="PhpStorm Project Wizard" height="300" style="max-width:100%;float:right;">

Select a model example template and subsequently give you project a name.
Through a click on the create-Button the required project structure becomes generated containing source folders 
for your models (*src*) and for the code generated based on your models (*src-gen*). The chosen example model 
is created within the src folder which can be used for a straightforward introduction.

<img src="img/php_pw_2.png" alt="PhpStorm Project Wizard 2" height="300" style="max-width:100%;float:right;">


### 2. Create a model ###
eJSL allows you the definition of different parts of a Joomla extension. Starting with the definition 
of a data structure (***entities***) on to its presentation (***pages***) up to the specification of 
Joomla-specific ***extensions***.

While using the text-based editor you get support by the code completion typing ***Ctrl + Space***.

For an easier start we recommend the use of the example instances, provided by the project wizards.  

### 3. Code generation ###
When you save your model, the code generator creates your modelled Joomla extensions within the project's 
src-gen folder. The extensions are installable within Joomla 3.x web sites and don't need any additional 
line of code. However, if you know what you do, you can extend the generated code through individual features. 
But beware: All the code within the src-gen folder becomes COMPLETELY overwritten, when you change your model 
and save it. Therefore we recommend to copy generated extensions to another folder within your project, where 
you can extend them without loosing them after a new code generation. Another and cleaner option is using a 
versioning tool like git to store your individual added code.

**Note:** Our tools are completly prototypical and we are currently working on the generator structure.

***
## Copyright ##
Copyright (C) 2013 - 2016, [iCampus](http://icampus.thm.de) - [Technische Hochschule Mittelhessen](http://www.thm.de). 
All rights reserved.
This project is distributed under the GPL (GNU General Public License) version 2. For further information see 
the [License details](https://git.thm.de/JooMDD/joomdd_repo/blob/master/LICENSE).

***
Please feel free to [contact](icampu@lists.thm.de) us, if you find some bugs or if you like to contribute to the project.
