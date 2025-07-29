# Configuration Helps

The `config.lua` file for the SS-Documents RedM script defines the configuration settings for creating, managing, and accessing documents within the game. Below is an explanation and example code illustrating the key parts of this configuration:

#### Key Configuration Elements

* **PaperItem**: This property specifies the item required to write a new document, which is set to `"cocoa"`.
* **Align**: This property sets the text alignment for documents, currently set to `"right"`.
* **Texts**: A table containing text identifiers and their respective string values, used for menu descriptions and document types. This allows customization and localization of different document-related texts.
* **AllowedDocs**: A dictionary that links each document category to specific job roles allowed to access or generate these documents. For example, the `"police"` category can be accessed by roles like `"PolitiaFederala"` and `"Maresal"`.
* **Documents**: This table defines the different document types, with each category containing specific documents, their titles, subtitles, and required form elements.

This code snippet demonstrates how to access and utilize the configuration settings to retrieve menu texts, validate access for different job roles, and interact with document information.
