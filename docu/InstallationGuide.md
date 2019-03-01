# Installation of JooMDD #
Please follow this installation guide to use JooMDD within [Eclipse](#eclipse), [PhpStorm](#PhpStorm), and [IntelliJ IDEA](#intellij-idea). 

Contents:
- [Installation of JooMDD](#installation-of-joomdd)
  - [Eclipse](#eclipse)
  - [PhpStorm](#phpstorm)
  - [IntelliJ IDEA](#intellij-idea)

## Eclipse ##
Install the JooMDD tools through the use of the following update site within the Eclipse update manager.

1. In Eclipse, go to <kbd>Help</kbd>-><kbd>Install New Software</kbd>
   
   <img src="img/eclipse_install_joomdd_tools_menu.png" alt="Eclipse install new Software item">

2. Then you can add the JooMDD update site via the <kbd>Add</kbd> button 
   
   <img src="img/eclipse_install_menu.PNG" alt="Eclipse software install menu">

3. Then you can specify an optional name and insert the path of the JooMDD update site as location. CLick <kbd>Add</kbd> to add the new repository.
   Please use the following URL as update site location:
 <https://raw.githubusercontent.com/icampus/JooMDD/master/Eclipse/JooMDDUpdateSite/site.xml>
   
   <img src="img/eclipse_add_repository_url.PNG" alt="Eclipse add repository">

4. In the next step you shoul see the eJSL plugin. Select it and click on <kbd>Next ></kbd>.
   
   <img src="img/eclipse_install_joomdd_software.PNG" alt="Eclipse select MDD of Joomla Extension">

5. Click on <kbd>Install anyway</kbd> to aloow the installation of our plugin and follow the installation dialogue.
   
   <img src="img/eclipse_install_repository_warning.PNG" alt="Eclipse warning while installing JooMDD">

6. To finish the installation you have to restart Eclipse. 

   <img src="img/eclipse_prompt_restart_eclipse.PNG" alt="Eclipse restart after installation">

7. After the restart, the plugin can be used to create your Joomla extension. Please see the [Getting started](GettingStarted.md) and [eJSL guide](eJSLGuide.md) documentation.

## PhpStorm ##
1. Install the *Xtext IDEA Core* and JooMDD plugin from our repository using the following JooMDD update site (alternatively you can download the plugins from this repository and install them manually into your IDE):
JooMDD update site (PhpStorm): <https://raw.githubusercontent.com/icampus/JooMDD/master/PhpStorm/ideaRepository/updatePlugins.xml>.
2. Restart PhpStorm.

## IntelliJ IDEA ##
1. Install the *Xtext IDEA Core* and JooMDD plugin from our repository using the following JooMDD update site (alternatively you can download the plugins from this repository and install them manually into your IDE):
JooMDD update site (IntelliJ IDEA): <https://raw.githubusercontent.com/icampus/JooMDD/master/IntelliJIDEA/ideaRepository/updatePlugins.xml>.
2. Restart IntelliJ.
