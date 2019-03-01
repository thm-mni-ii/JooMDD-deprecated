# eJSL Guide #

Contents:

- [eJSL Guide](#ejsl-guide)
  - [Main concepts: The conference example](#main-concepts-the-conference-example)
    - [Data modelling](#data-modelling)
    - [Interaction modelling](#interaction-modelling)
    - [Extension modelling](#extension-modelling)
    - [Generated code](#generated-code)
  - [Use the language](#use-the-language)
    - [General conventions](#general-conventions)
    - [Data modelling](#data-modelling-1)
      - [Entities](#entities)
      - [Attributes](#attributes)
      - [Types](#types)
      - [References](#references)
    - [Interaction modelling](#interaction-modelling-1)
      - [StaticPage](#staticpage)
      - [IndexPage](#indexpage)
      - [DetailsPage](#detailspage)
      - [CustomPage](#custompage)
    - [Extension modelling](#extension-modelling-1)
      - [Manifestation](#manifestation)
      - [Language support](#language-support)
      - [Extension types](#extension-types)
        - [Packages](#packages)
        - [Components](#components)
        - [Modules](#modules)
        - [Plugins](#plugins)
        - [Templates #####](#templates)
        - [Libraries](#libraries)
      - [Extension interaction](#extension-interaction)
  - [Example models](#example-models)
    - [Conference](#conference)
    - [Shop](#shop)
    - [Generic example model](#generic-example-model)

##  Main concepts: The conference example ##

The eJSL language is a textual modelling language which is based on three main modelling parts - data, interaction, and extension modelling. Within the next sections, we will illustrate the language features by using the conference eJSL model. This model can be used as example model in the IDE plugins and the web editor to generate a conference component on the fly without any manual refinements. 

**(Please visit the getting started guides for [IDE](GettingStarted.md) and [Web editor](WebEditorGettingStarted.md) to find information regarding the use of the model editors.)

The generated conference component consists of a set of frontend and backend views for participants, talks, rooms, and the conference programme. Once installed, the views allow CRUD operations on the attributes which are illustrated within list tables and details views.

<img src="img/conference_J3.png" alt="J3 Conference Component" style="max-width:100%">

To understand the main concept of the language we take a partial look at the conference model.

```
eJSLModel "Conference" {
    eJSL part: CMS Extension {
        entities {...}    // Data modelling
        pages {...}       // Interaction modelling
        extensions {...}  // Extension modelling 
    }
}

```

In order to generate a deployable Joomla extension, all model parts have to be defined. The entity section contains the whole data modelling of your project. It allows the definition of data entities with typed attributes and references to attributes of the other entities.

### Data modelling ###

The entities part of the conference model consists of data entities which are required for a simple conference:

```
entities {
    Entity Participant {...}
    Entity Talk {...}
    Entity Room {...}
    Entity Programme {...}
}
```
All **entities** must have unique identifiers to allow cross-references within the model file. For each entity, **attributes** can be added. These attributes must be defined with a **type**. The language provides a set of type abstractions like Text, Short_Text, Boolean, Integer, Date, or File. For these types, a sophisticated type mapping is processed during code generation. However, it is also possible to define own types, which can be assigned during an attribute definition. For further reading, see the [type documentation](#types) below.

```
Entity Participant {                 // Entity definition with identifier
    attributes {
        Attribute name {             // Attribute definition with identifier
            type = Short_Text        // Attribute type
        }
        Attribute affiliation {
            type = Text
        }
        Attribute nationality {
            type = Text
        }
    }
}
```
 All entities must at least contain one attribute. For defined attributes, references can be defined within an entity definition. These references allow relationships between different entities. In the example above, a reference is defined for the `speaker` attribute of the `talk` entity. It references the `name` attribute of the `Participant` entity. It is also to define reference multiplicities (`min`, `max`), whereby min can be '0' or '1' and max can be defines as '1' or '-1' (corresp. to 'n' or '*' ).
```
Entity Talk {
    attributes {
        Attribute title {
            type = Short_Text
        }
        Attribute ^description              // Some identifiers need the '^' prefix, since they are also used as language keywords
            type = Text
        }
        Attribute speaker {
            type = Text
        }
    }
    references {
        Reference {                                          // Reference definition
            EntityAttribute = speaker                        // There ference attribute of the entity
            ReferencedEntity = Participant                   // Identifier of the referenced entity
            ReferencedEntityAttribute = Participant.name     // Referenced attribute
            min = 1                                          // Reference multiplicity (lower)
            max = 1                                          // Multiplicity (upper)
        }
    }  
}
```
 For a better understanding, see the following class diagram which illustrates the attributes of and references between the conference entities.
        
<img src="img/conferenceModel.png" alt="Conference Model" style="max-width:100%">

### Interaction modelling ###

The **pages** section represents an abstraction layer for the MVC structure of Joomla components. I.e. an explicit definition of models, views, and controllers is not required. 

If you don't want to change much in the generated code and use the views as they are, we recommend to make use of the two dynamic page types `IndexPage` and `DetailsPage`. 

```
pages {
    IndexPage Participants {...}
    DetailsPage Participant {...}
    IndexPage Talks {...}
    DetailsPage Talk {...}
    IndexPage Rooms {...}
    DetailsPage Room {...}
    IndexPage Programme {...}
    DetailsPage Session {...}
}
```
Index pages can be used to define the representation of one or more entity attributes in a tabular list view. If a page is then referenced by a component (in the extension modelling part), all the required MVC code will be generated. If you want to reuse the page for frontend and backend of your component, you can reference it several times in the extension definition. Additionally, you can refer the same page by a module to use it for the module representation. This is one of the biggest strengths of JooMDD in contrast to other code generators. 

<img src="img/conference_J3_backend_page.png" alt="Conference backend list" style="max-width:100%">

```
IndexPage Participants {                // Will be interpreted as list view
    *Entities Participant               // Which entity will be presented in the list?
    representation columns = Participant.name, Participant.address, Participant.affiliation             // (optional) selection of list columns
    filters = Participant.name, Participant.affiliation     // Filters for Search tools support
    links {                             // Link definition to enable interaction between views
        InternalcontextLink Details {   
            target = Participant                                    // Link to details page
            linked attribute = Participant.name                     // Attribute which is used as link
            linkparameters {
                Parameter name = *Attribute  "Participant.name"     // Send participant's name as request param
            }
        }
    }
}
```
Pages require at least one entity as reference, which will then be represented in the view. If desired, the table `representation columns` of the view can be specified. However, this step is optional - If no columns specified, all entity attributes will be shown as columns. If required, you can specify `filters` for the fields, which later can be used as part of the Seach Tools (filters).

To enable interaction between views, `links` can be specified. All you need is to specify the target page and the field which will act as link. In the example above, the participant's `Name` field is used as link to the `Participant` page, which is a details page (see below). The eJSL language provides static and context links, whereas context links allow the definition of request parameters. In the example above the participants name is specified as request parameter for the link. So, it will be used as GET parameter for the link(additionally to an autogenerated ID parameter).

<img src="img/conference_link_param.png" alt="Conference backend list" style="max-width:100%">

<br> <br>
In contrast to IndexPages, the eJSL language can be used to specify `DetailsPages`. This page type can be used to model details and/or edit views. DetailsPages can be referenced by different extension, too. So, they can be used as editable details view in the backend of a Joomla component, non-editable details view in the fronten, or as details representation within a Joomla module - only defined once in the pages section.

<img src="img/conference_J3_backend_page_details.png" alt="Conference backend details page" style="max-width:100%">

**Above:** Editable backend view for participant details

**Below:** Non-editable frontend view for participants details
<img src="img/conference_J3_frontend_page_details.png" alt="Conference frontend details page" style="max-width:100%">

```
DetailsPage Pattern {
    *Entities Pattern               // Which entity will be presented in the details view?
    links {
        InternalLink Index {
            target = Patterns       // Link to index page
            linked attribute = name 
        }
    }
}
```
The specification of a `DetailsPage` is more frugal - particularly if they are used together with IndexPages. All they need is the entity which is represented and a link back to an IndexPage to support actions like **Close** and **Save & Close** in a generated component.

In addition to the `IndexPage` and `DetailsPage` page types, the eJSL language provides further page definitions. For further information see the [Interaction modelling](#interaction-modelling) section below.

### Extension modelling ###

Within the extension section of an eJSL model, the modelled pages and entities can be integrated into extension-specific structures. In combination wit meta information like authors or copyright, and language assignment, extensions can be specified. Supported extension types are **packages**, **components**, **modules**, **plugins**, **templates**, and **libraries**. In the conference model, a component as the most sophisticated extension type is modelled. How to use other extension types is explained in the [extension modelling](#extension-modelling) section below.
```
extensions {
    Component MyConference {
        Manifestation {...}
        languages {...}
        sections {...}
    }
}   
```
In the conference example, a component is modelled. A `Component` model requires meta information which will mainly feed into the manifest of a component. This model part is similar for all extension types which are supported by the eJSL language. In addition, the supported languages can be specified. However, the main information for the code generator is specified in the `sections` part. This part contains the references to existing `pages` which in turn will result in MVC code within the componenten.
```
Manifestation {
    authors {
        Author "John Doe" {
            authoremail = "john.doe@example.org"
        }
    }
    copyright = "Copyright (C) 2019 All right reserved."
    license = "GNU General Public License"
    version = "1.0.1"
}  
```
The manifestation part of the conference is very straight forward. Besides `authors`, meta information like `copyright`, `license`, or `version` can be specified.
```
languages {
    Language de-DE {}   // Create language files for german language
    Language en-GB {}   // Create language files for british english language
}
```
Specifying languages enables multi language support in an extension. All you need to do is to specify the language key (e.g. `en-GB`). The generator then creates the respective language files filled with the used language key and english(!) values. Therefore, you have to translate the values after the code generation process. However, to avoid a manual refinement in the generated code, you can specify key-value pairs within the respective language definition. For further information see the extensive [language](#language-support) description below.
```
sections {
    Frontend section {              // Here you specify the pages which will be used as frontend views
        *Pages {
            *Page : Participants
            *Page : Talks
            *Page : Rooms
            *Page : Programme
        }
    }
    Backend section {               // Here you specify the pages which will be used as backend views
        *Pages {
            *Page : Participants
            *Page : Participant
            *Page : Talks
            *Page : Talk
            *Page : Rooms
            *Page : Room
            *Page : Programme
            *Page : Session
        }
    }
}
```
The core part of a component specification is placed within the `section` definition. Here you can specify which pages you will use in which part (frontend/backend) of the component. In the example, all defined pages are referenced in the backend section, whereas the `IndexPages` are also referenced in the frontend section. This information is sufficient for a sophisticated code generation of both section with all required files. Based on presented example, all further generated views will have their own model and controller file. However, it is also possible to specify a reuse of models - e.g. if the frontend view shall use the backend model. For further information of possible dependency modelling see the [Extension interaction(#extension-interaction)] section of this site.

### Generated code ###
<img src="img/conference_file_structure.png" alt="Conference file structure" style="max-width:100%; float:right;">

Based on the example conference model, a component can be generated which can directly installed to a running Joomla instance. 

The generated structure complies to the file structure of installed extension in a Joomla-based site. This allows copy&paste of new code after a new generation step (e.g. after model refinements).


<img src="img/conference_file_structure_admin.png" alt="Conference file structure" style="max-width:100%">

## Use the language ##
### General conventions ###
- **Some keywords are reserved in the language**. In this case, the validator throws an validation error, if they are used as identifier. However, you can **use the caret operator (^) as prefix** to allow their usage. The generator then removes the prefix during code compilation to ensure clean identifiers in the generated extension code. <br><br>
  `Attribute template` -> Validation Error <br>
  `Attribute ^template` -> Valid model

### Data modelling ###
#### Entities ####
#### Attributes ####
#### Types ####
#### References ####
### Interaction modelling ###
#### StaticPage ####
#### IndexPage ####
#### DetailsPage ####
#### CustomPage ####
### Extension modelling ###
#### Manifestation ####
#### Language support ####
#### Extension types ####
##### Packages #####
##### Components #####
##### Modules #####
##### Plugins #####
##### Templates ##### 
##### Libraries #####
#### Extension interaction ####
## Example models ##
### Conference ###
### Shop ###
### Generic example model ###
