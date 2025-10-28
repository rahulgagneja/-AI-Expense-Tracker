🤖AIExpenseTracker

Anintelligentexpensetrackingsystembuiltwithn8nthatautomaticallyprocessesandrecordsyourexpensesthroughnaturalconversation.Simplychataboutyourpurchases,andtheAIhandlestherest!

![n8nWorkflow](https://img.shields.io/badge/n8n-Workflow-orange)
![OpenAI](https://img.shields.io/badge/OpenAI-Powered-green)
![GoogleSheets](https://img.shields.io/badge/Google%20Sheets-Integration-blue)

✨Features

-💬ConversationalInterface:Naturallanguageinputviachattrigger
-🧠SmartFieldExtraction:AIAgentautomaticallyparses:
-Transactiontype(Credit/Debit)
-Expensecategory
-Amount
-Runningtotalbalance
-📊AutomatedRecording:DirectintegrationwithGoogleSheets
-🚨LowBalanceAlerts:Automaticemailwhenbalance<₹10,000
-✨BeautifulFormatting:ChatModeloptimizesresponsesfor:
-User-friendlychatreplies
-CleanGoogleSheetsentries
-ProfessionalGmailnotifications
-💾ContextRetention:SimpleMemorymaintainsconversationflowandbalancetracking

🏗️Architecture

Theworkflowconsistsoffivemaincomponents:

1.ChatTrigger-Receiveschatmessagesfromusers
2.AIAgent-ProcessesnaturallanguageusingOpenAI
3.SimpleMemory-Storesconversationcontextandbalancedata
4.GoogleSheets-Recordsexpensetransactions
5.Gmail-Sendsnotificationemailsforimportantalerts

🔄WorkflowProcess

```
UserInput→AIAgent(ExtractFields)→GoogleSheets(Record)→BalanceCheck→
GmailAlert(if<10000)→ChatModel(FormatResponse)→User
```

1.ChatTrigger:Usersendsamessageabouttransaction(e.g.,"Iboughtphoneof112000")
2.AIAgent:Extractsandstructuresdataintofields:
-Credit/Debit
-TypeofExpense
-Amount
-TotalBalance
3.GoogleSheets:Recordsthetransactionwithallfields
4.ConditionalCheck:Ifbalancedropsbelow10,000
5.Gmail:Sendslowbalancealertemailwithformattedmessage
6.OpenAIChatModel:Optimizesandbeautifiestheresponsefor:
-Userchatreply
-GoogleSheetsentryformatting
-Gmailnotificationtext
7.SimpleMemory:Maintainsconversationcontextandrunningbalance

📋Prerequisites

-[n8n](https://n8n.io/)instance(cloudorself-hosted)
-OpenAIAPIkey
-GoogleAccountwithSheetsAPIaccess
-GmailAPIcredentials

🚀SetupInstructions

1.ClonetheWorkflow

ImporttheworkflowJSONintoyourn8ninstance:
-Downloadtheworkflowfile
-Goton8n→Workflows→ImportfromFile
-SelectthedownloadedJSON

2.ConfigureCredentials

Setupthefollowingcredentialsinn8n:

OpenAIAPI
-NavigatetoCredentials→AddCredential→OpenAI
-EnteryourOpenAIAPIkey

GoogleSheets
-AddGoogleOAuth2credentials
-AuthorizeaccesstoGoogleSheets

Gmail
-AddGmailOAuth2credentials
-Authorizeaccesstosendemails

3.SetUpGoogleSheet

CreateaGoogleSheetwiththefollowingcolumns(asextractedbyAIAgent):

|Date|Credit/Debit|TypeofExpense|Amount|Total|
|------|--------------|-----------------|-----

4.ConfigureWorkflowNodes

ChatTrigger
-Setupyourpreferredchatinterface
-Configurewebhookormessagingplatform

AIAgent(FieldExtractor)
-Createprompttoextract:Credit/Debit,TypeofExpense,Amount,Total
-Examplepromptstructure:
```
Extractthefollowingfromuserinput:
-IsthisaCreditorDebit?
-Whattypeofexpenseisthis?
-Whatistheamount?
-Calculatethenewtotalbalance
```

GoogleSheetsNode
-Linktoyourexpensetrackingspreadsheet
-Mapextractedfieldstosheetcolumns

ConditionalNode
-Setcondition:`TotalBalance<10000`
-RoutestoGmailwhenconditionistrue

OpenAIChatModel
-Configuretooptimizeandformatresponses
-Usedforbeautifying:
-Chatrepliestouser
-GoogleSheetsdataentries
-Gmailalertmessages

GmailNode
-Setrecipientemailaddress
-UseformattedtextfromChatModel

SimpleMemory
-Initializewithstartingbalance
-Configuretostoreconversationcontext

5.ActivateWorkflow

-Click"Activate"inthetoprightcorner
-Theworkflowisnowreadytoprocessexpenses!

💡UsageExamples

Simplychatwiththesystemnaturally:

```
"Iboughtaphonefor112000"
→Records:Debitof112000,updatesbalanceto-104000,sendslowbalancealert

"Spent500ongroceries"
→Records:Debitof500inGroceriescategory

"Receivedsalaryof50000"
→Records:Creditof50000,updatesbalance
```

🎯KeyComponents

1.ChatTrigger
-Entrypointforusermessages
-Capturesnaturallanguagetransactioninputs

2.AIAgent(FieldExtractor)
-Purpose:Parsesuserinputintostructuredfields
-OutputFields:
-Credit/Debitclassification
-Typeofexpense(category)
-Amount
-Totalbalance(runningcalculation)
-Example:"Iboughtphoneof112000"→{type:"Debit",category:"Electronics",amount:112000,balance:-104000}

3.GoogleSheetsIntegration
-Recordsstructuredtransactiondata
-Maintainsexpensehistorywithallextractedfields
-Updatesrunningbalanceautomatically

4.ConditionalLogic(BalanceMonitor)
-Checksifbalance<₹10,000
-Triggersalertworkflowwhenthresholdisbreached

5.OpenAIChatModel(ResponseOptimizer)
-Triple-purposeformatting:
-Craftsuser-friendlychatresponses
-FormatsdatabeautifullyforGoogleSheetsentries
-GeneratesprofessionalGmailnotificationtext
-Ensuresconsistent,polishedcommunicationacrossallchannels

6.GmailNotification
-Sendsformattedlowbalancealerts
-UsesoptimizedtextfromChatModel
-Keepsyouinformedaboutaccountstatus

7.SimpleMemory
-Storesconversationcontext
-Tracksrunningbalancebetweenmessages
-Enablescontinuityacrossmultipletransactions

📊SampleOutput

Whenyouloganexpense:

```
Input:"Iboughtphoneof112000"

Output:"Thepurchaseofthephonefor112000hasbeenrecorded
asaDebit,andthenewtotalbalanceis-104000.Analertemail
hasbeensenttoyouregardingthelowbankbalance."
```

🔧Customization

ModifyAlertThreshold
Updatetheconditionnodetochangewhenlowbalancealertstrigger

AddCategories
EnhancetheAIprompttorecognizecustomexpensecategories

ChangeMemoryStructure
ModifytheSimpleMemorynodetostoreadditionalfields

CustomEmailTemplates
EdittheGmailnodetopersonalizenotificationmessages

📈FutureEnhancements

-Addsupportformultiplecurrencies
-Implementexpenseanalyticsandinsights
-Createmonthly/weeklyspendingreports
-Addreceiptimageprocessing
-Supportformultiplebankaccounts
-Budgettrackingandwarnings
-Exportfunctionality(PDF,CSV)

🐛Troubleshooting

Workflownottriggering?
-Ensuretheworkflowisactivated
-Checkchatinterfaceconnectivity

AInotextractingdatacorrectly?
-ReviewOpenAIAPIkeyvalidity
-AdjustAIpromptforbetteraccuracy

Sheetsnotupdating?
-VerifyGoogleSheetscredentials
-Checksheetpermissions

📝License

MITLicense-feelfreetouseandmodifyforyourneeds
