Exception Handling


Handling Exception is writing a code to gracefully recover from an error. 
	You "try" to run your code. If there is an exception, you "catch" it and can run some code, then you can "finally" run some code whether you had an exception or not.

  - How to catch Exception
  - How to show Exception message
  - How to handle Exception in Lightnig Component


 How To Catch Exeption!
 Method 1:
 
			try{
			 update accounts;
			} catch (DMLException e){
			 for (Account account : accounts) {
				  account.addError('There was a problem updating the accounts');
			 }
			} finally {
			 inProgress = false;
			}

 Method 2:
 
			Database.SaveResult[] lsr = Database.update(accounts, false); 
            			for(Database.SaveResult sr : lsr){ 
            			if (!sr.isSuccess()) { 
            				myMethodToaddToErrorObjectList(sr);
            			}
			} 
			myMethodToaddToErrorObjectList(SObject account)
			{
				for (Account account : accounts) {
				account.addError('There was a problem updating the accounts');
												 }		
			}

How To Display or Notify Exception  / Error Message !


 On a visualforce page :-

			ApexPages.Message myMsg = new ApexPages.Message(ApexPages.Severity.FATAL,'my error msg');
			ApexPages.addMessage(myMsg);

 Send An Email :-

			try{
			 update account;
			} catch (DMLException e){
			 ApexPages.addMessages(e);
			 Messaging.SingleEmailMessage mail=new Messaging.SingleEmailMessage();
			 String[] toAddresses = new String[] {'developer@acme.com'};
			 mail.setToAddresses(toAddresses);
			 mail.setReplyTo('developer@acme.com');
			 mail.setSenderDisplayName('Apex error message');
			 mail.setSubject('Error from Org : ' + UserInfo.getOrganizationName());
			 mail.setPlainTextBody(e.getMessage());
			 Messaging.sendEmail(new Messaging.SingleEmailMessage[] { mail });
			}

 Logging in a custom object :-

			try{
			 throw new MyException('something bad happened!');
			} catch (MyException e){
			 ApexPages.Message myMsg = new ApexPages.Message(ApexPages.Severity.FATAL,'my error msg');
			 futureCreateErrorLog.createErrorRecord(e.getMessage());
			}
			global class futureCreateErrorLog {
			 @future
			 public static void createErrorRecord(string exceptionMessage){
				 myErrorObj__c newErrorRecord = new myErrorObj__c();
				 newErrorRecord.details__c = exceptionMessage;
				 Database.insert(newErrorRecord,false);
			 }
			}

 Displaying in a Lightning Component :-

			({
			throwErrorForKicks: function(cmp) {
				// this sample always throws an error to demo try/catch
				var hasPerm = false;
				try {
					if (!hasPerm) {
						throw new Error("You don't have permission to edit this record.");
					}
				}
				catch (e) {
					$A.createComponents([
						["ui:message",{
							"title" : "Sample Thrown Error",
							"severity" : "error",
						}],
						["ui:outputText",{
							"value" : e.message
						}]
						],
						function(components, status, errorMessage){
							if (status === "SUCCESS") {
								var message = components[0];
								var outputText = components[1];
								// set the body of the ui:message to be the ui:outputText
								message.set("v.body", outputText);
								var div1 = cmp.find("div1");
								// Replace div body with the dynamic component
								div1.set("v.body", message);
							}
							else if (status === "INCOMPLETE") {
								console.log("No response from server or client is offline.")
								// Show offline error
							}
							else if (status === "ERROR") {
								console.log("Error: " + errorMessage);
								// Show error message
							}
						}
					);
				}
			}
			})

Custom Exception From Server Apex to Client Side

			public with sharing class SimpleErrorController {
			static final List<String> NAUGHTY_WORDS = new List<String> {
				'naughty',
				'words'
			};
			@AuraEnabled
			public static String helloOrThrowAnError(String name) {
				// Make sure we're not seeing something naughty
				for(String badWordStem : NAUGHTY_WORDS) {
					if(name.containsIgnoreCase(badWordStem)) {
						// How rude! Gracefully return an error...
						throw new AuraHandledException('NSFW name detected.');
					}
				}
				// No bad word found, so...
				return ('Hello ' + name + '!');
			}
			}
