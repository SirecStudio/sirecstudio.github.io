# Configuration File

{% code overflow="wrap" %}
```lua
Config = {
    
PaperItem = "paperitem", -- Paper item to start write a new document
Align = "right", 
    
Texts = {
    ["main_menu"] = "Documents",
    ["main_menu_desc"] = "Useful Documents",

    --If you create a category of documents, create a TRANSLATE too, like if you create "medic", add ["medic"] = "Medic Documents" and ["medic_desc"] = "Medic Documents"
    ["public"] = "Public Documents",
    ["public_desc"] = "Official public documents",
    ["police"] = "Police Documents",
    ["police_desc"] = "Official police documents",
    ["primar"] = "Town Hall Documents",
    ["primar_desc"] = "Municipal documents",
    ["guvernator"] = "Government Documents",
    ["guvernator_desc"] = "Official government documents",
    ["maresal"] = "Marshal Documents",
    ["maresal_desc"] = "High-rank police documents",

    ["showdoc"] = "Show Document",
    ["showdoc_desc"] = "Show the document to someone",
    ["viewdoc"] = "View Document",
    ["viewdoc_desc"] = "View the document",
    ["nobody_around"] = "There is nobody around!",
    ["save_document"] = "Document signed and saved !",
},

    
AllowedDocs = {
	--["CATEGORY OF DOCS"] = {"Job1", "Job2"}
	["guvernator"] = {"PolitiaFederala", "Guvernator"},
	["primar"] = {"PolitiaFederala", "Guvernator", "PrimarRhodes", "PrimarValentine", "PrimarBlackWater"},
	["maresal"] = {"PolitiaFederala", "Guvernator", "Maresal"},
	["police"] = {"PolitiaFederala", "Maresal", "Detectiv", "PolitieFrontiera", "OfiterValentine", "SerifValentine", "OfiterAnnesburg", "SerifAnnesburg", "OfiterRhodes", "SerifRhodes", "OfiterBlackWater", "SerifBlackWater"},
	["medic"] = {"MedicRezidentRH", "MedicRezidentBW", "MedicRezidentVAL", "MedicRezidentSD", "MedicSpecialistRH", "MedicSpecialistBW", "MedicSpecialistVAL", "MedicSpecialistSD", "MedicPrimar", "Shaman", "OfiterMedicalVAL", "OfiterMedicalRH", "OfiterMedicalBW", "OfiterMedicalSD"},
},

Documents = {
    ["guvernator"] = {
        {
            Tittle = "POLITICAL AFFILIATION CERTIFICATE",
            subTittle = "Official document certifying active membership in a political party.",
            InformationSubTittle = "Validated and issued by the Territorial Electoral Council.",
            elements = {
                { label = "FULL NAME OF THE MEMBER:", type = "input", value = "",  },
                { label = "POLITICAL PARTY:", type = "input", value = "",  },
                { label = "POSITION OR STATUS:", type = "input", value = "",  },
                { label = "VALID UNTIL:", type = "date", value = "",  },
                { label = "NOTES", type = "textarea", value = "It is hereby confirmed that the above-mentioned citizen holds no criminal record and is legally eligible to participate in political activities. This certificate confirms their legal registration as an active member of a recognized political party within West Frontier territory.", can_be_emtpy = true }
            }
        },
        {
            Tittle = "PARDON CERTIFICATE",
            subTittle = "Official document regarding the annulment of a criminal sentence.",
            InformationTittle = "Issued by the competent authority under Law no. 105 - Pardon.",
            InformationSubTittle = "Through this document, the sentence imposed upon the mentioned individual is officially annulled, granting them release from custody and legal rehabilitation within West Frontier.",
            elements = {
                { label = "NAME OF THE CONVICT:", type = "input", value = "",  },
                { label = "DATE OF CONVICTION:", type = "date", value = "",  },
                { label = "REASON FOR CONVICTION:", type = "input", value = "",  },
                { label = "DATE OF PARDON:", type = "date", value = "",  },
                { label = "ADDITIONAL REMARKS", type = "textarea", value = "The citizen is hereby fully pardoned and has no remaining obligations toward the judicial system related to this conviction. Their criminal record shall be marked as 'legally pardoned'.", can_be_emtpy = true }
            }
        },
    },

    ["public"] = {
        {
            Tittle = "OFFICIAL STATEMENT",
            subTittle = "Legal statement given by a witness to an event.",
            InformationSubTittle = "The undersigned declares under their own responsibility that the information below is true, accurate, and corresponds to reality. This statement is given for official purposes and may be used as legal evidence before the territorial authorities of West Frontier.",
            elements = {
                { label = "Date:", type = "date", value = "",  },
                { label = "Event Description / Testimony", type = "textarea", value = "",  }
            }
        },
        {
            Tittle = "DENUNCIATION STATEMENT",
            subTittle = "Official report to legal authorities.",
            InformationSubTittle = "The person below declares, under personal signature, the facts or individuals involved in an illegal action.",
            elements = {
                { label = "PERSON'S LAST NAME:", type = "input", value = "",  },
                { label = "PERSON'S FIRST NAME:", type = "input", value = "",  },
                { label = "DATE OF EVENT:", type = "input", value = "",  },
                { label = "LOCATION OF INCIDENT:", type = "input", value = "",  },
                { label = "DESCRIPTION OF THE ACT:", type = "textarea", value = "",  },
            }
        }
    },

    ["primar"] = {
        {
            Tittle = "SALES DECLARATION",
            subTittle = "Sales agreement between two citizens.",
            InformationSubTittle = "This statement confirms the transfer of an asset between two parties, by mutual agreement.",
            elements = {
                { label = "BUYER'S NAME:", type = "input", value = "",  },
                { label = "SELLER'S NAME:", type = "input", value = "",  },
                { label = "SALE PRICE:", type = "input", value = "",  },
                { label = "TRANSACTION DATE:", type = "date", value = "",  },
                { label = "DESCRIPTION OF THE ASSET:", type = "textarea", value = "",  },
            }
        },
        {
            Tittle = "DEBT DECLARATION",
            subTittle = "Acknowledgment of debt between citizens.",
            InformationSubTittle = "The debtor acknowledges owing a financial debt to the creditor.",
            elements = {
                { label = "DEBTOR'S NAME:", type = "input", value = "",  },
                { label = "CREDITOR'S NAME:", type = "input", value = "",  },
                { label = "AMOUNT OWED:", type = "input", value = "",  },
                { label = "DUE DATE:", type = "date", value = "",  },
                { label = "NOTES:", type = "textarea", value = "", can_be_emtpy = true },
            }
        },
        {
            Tittle = "TEMPORARY EMPLOYMENT CONTRACT",
            subTittle = "Service agreement between two parties.",
            InformationSubTittle = "The undersigned parties agree to enter a contract for temporary employment.",
            elements = {
                { label = "EMPLOYER'S NAME:", type = "input", value = "",  },
                { label = "WORKER'S NAME:", type = "input", value = "",  },
                { label = "TYPE OF WORK:", type = "input", value = "",  },
                { label = "CONTRACT DURATION:", type = "input", value = "",  },
                { label = "AMOUNT PAID:", type = "input", value = "",  },
            }
        },
        {
            Tittle = "MARRIAGE CERTIFICATE",
            subTittle = "Legal agreement between two individuals to form a family.",
            InformationSubTittle = "By signing this document, both parties are legally married in accordance with local laws.",
            elements = {
                { label = "HUSBAND'S NAME:", type = "input", value = "",  },
                { label = "WIFE'S NAME:", type = "input", value = "",  },
                { label = "DATE OF MARRIAGE:", type = "input", value = "",  },
                { label = "CEREMONY LOCATION:", type = "input", value = "",  },
                { label = "WITNESS NAME:", type = "input", value = "",  },
                { label = "WITNESS NAME:", type = "input", value = "",  },
            }
        },
        {
            Tittle = "DIVORCE AGREEMENT",
            subTittle = "Mutual termination of marriage between two individuals.",
            InformationSubTittle = "The parties below freely and knowingly consent to the dissolution of their existing marriage.",
            elements = {
                { label = "HUSBAND'S NAME:", type = "input", value = "",  },
                { label = "WIFE'S NAME:", type = "input", value = "",  },
                { label = "DATE OF DIVORCE:", type = "input", value = "",  },
                { label = "SIGNING LOCATION:", type = "input", value = "",  },
                { label = "WITNESS NAME:", type = "input", value = "",  },
                { label = "WITNESS NAME:", type = "input", value = "",  },
            }
        },
    },

    ["maresal"] = {
        {
            Tittle = "SEARCH WARRANT",
            subTittle = "Official permission to conduct a search.",
            InformationSubTittle = "Issued under Article 3 of the West Frontier Constitution.",
            elements = {
                { label = "NAME OF PERSON/LOCATION TO BE SEARCHED:", type = "input", value = "",  },
                { label = "DATE OF AUTHORIZATION:", type = "date", value = "",  },
                { label = "DETAILS ABOUT THE SEARCH TARGET", type = "textarea", value = "",  }
            }
        },
    },

    ["police"] = {
        {
            Tittle = "FIREARM LICENSE",
            subTittle = "Special permit to carry a firearm issued by legal authorities.",
            InformationSubTittle = "Official document issued in accordance with territorial regulations.",
            elements = {
                { label = "HOLDER'S FIRST NAME:", type = "input", value = "",  },
                { label = "HOLDER'S LAST NAME:", type = "input", value = "",  },
                { label = "VALID UNTIL:", type = "date", value = "",  },
                { label = "FIREARM SERIAL NUMBER:", type = "input", value = "Optional",  },
                { label = "ADDITIONAL INFORMATION", type = "textarea", value = "The above-mentioned citizen is authorized and granted the legal right to own and use a firearm, under the conditions provided by law, until the stated expiration date.",  }
            }
        },
    },
} -- END DOCUMENTS
}



```
{% endcode %}

