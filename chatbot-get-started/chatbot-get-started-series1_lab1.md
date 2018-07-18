# Oracle Intelligent Bots Training	


**Meet a Chatbot	**

In this lab, you’ll examine, explore and test a financial banking chatbot. The chatbot, called MasterBot, allows users to find balances in their banking accounts, transfer money between banking accounts, and send money to different people and accounts.

**Before You Begin**

To complete the labs, you will need access to Oracle Mobile Cloud, Enterprise (OMCe). To help you build your chatbots, you will use a set of files that contain code that’s referenced in the instructions. These files are contained in the labfiles.zip file. Before beginning this exercise, download and unzip this file. Save it to a convenient place because you’ll be referring to it throughout this course. 

**Step 1: Test the Get Balance Function**

In this section, you’ll take a look at a banking chatbot named MasterBot. This is a complete chatbot that you will reconstruct during the course. In this section, you will focus on testing its Get Balance function.

1.	Log in to your OMCe instance. 

2.	In the left navbar, click Mobile Apps and then select Bots.

![<picture 1-1>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/1-1.jpg)



The landing page appears, which displays a catalog of the chatbots that were created on this instance.


3.	In the Filter field, enter MasterBot.

![<picture 1-2>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/1-2.jpg)

The MasterBot tile should appear in the filtered list of bots. If you can’t find it, it’s probably because it hasn’t been loaded into your instance. If this happens, you can create this chatbot quickly by first clicking the Import Bot button and then navigating to, and selecting, the MasterBot.json file that’s located in the labfiles/code directory of the labfiles.zip file. 
 
 
![<picture 1-3>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/1-3.jpg)

**Note:** If you ever need to clone, export, or delete the chatbot, you can find these functions from the drop down hamburger menu located in the lower right of the tile. You can also extract a log of this chatbot’s previous conversations for future reference. You won't need to use these functions now, but just know they are here when you do need them.

![<picture 1-4>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/1-4.jpg)

4.	Click the MasterBot tile to see the chatbot details. 

![<picture 1-5>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/1-5.jpg)
 
 You can now take a look at the various parts of the chatbot and see how it was designed.  On the left, you can see the navbar, which displays a vertical list of icons that allow you to work on the chatbot's intents, entities, flow, components, and settings. Each icon that you click navigates you to that portion of the chatbot's design.  
 
 
 5.	Click the Intent button (the flag) in the left navbar and then select the Balances intent.
 
![<picture 1-6>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/1-6.jpg)
  

On the top far right, notice the Play icon (that white triangle pointing to the right). This is the button you use to test the chatbot. Click the Play button.


6.	A test pane (the Tester) opens, where you can enter text messages and send them to the chatbot.  The chatbot’s replies display above the Messages area. 

**Note:**  If you've just imported the chatbot, then you need to click the Train button before you chat with it.

**Tip:** The Reset button allows you to exit any chatbot conversation and start over. If you want to dismiss the test pane, just click the Play icon.
 
![<picture 1-7>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/1-7.jpg)



7.	In the message area, type in What's my balance? and then click the Send button.
 
![<picture 1-8>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/1-8.jpg)


8.	The chatbot recognizes that the request is about balances, and to enable it to return an amount, it needs to know the type of account. The chatbot then displays the accounts that it knows about and allows you to select the one you want. You could either type the value in to the Message area, or select it using your mouse.


9.	Select one of the accounts. The chatbot returns the balance amount for that account.
 
![<picture 1-9>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/1-9.jpg)

10.	If you would have included the account type in the initial request, then the chatbot would have returned the amount without any prompting for the account. So, try that out by entering What’s my savings balance? and then click Send

**Tip:** Finish each round of questions and answers, or click the Reset button to create a new session. Doing this avoids confusion with an incomplete flow from a previous session

![<picture 1-10>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/1-10.jpg)


A message is returned showing the balance amount for a specific account type.
 
![<picture 1-11>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/1-11.jpg)


11.	Try some other phrases of your own that are associated with retrieving a bank balance to see how effective they are. Enter phrases like:


- How much do I owe on my credit card? 	
- How much money do I have in checking? 	
- What’s my available credit on my Amex? 
- What’s the current balance on my Chase account?


**Tip:** Remember to click Reset.


**Step 2: Test the Send Money Function**

In this section, you test the ability of the MasterBot to send money from a bank account to someone. Like the bank accounts, you select the recipients from a predefined list.

1.	Let's first see how the chatbot responds to a simple version of the request, with the chatbot driving the interaction by issuing prompts.

Click the Reset button. Next, enter Send Sasha money and then click Send.
 
![<picture 2-1>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/2-1.jpg)
 
2.	The first thing the chatbot needs to know is: which account do you want the money to come from, so select an account.
 
![<picture 2-2>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/2-2.jpg)
 
3.	The last bit of info the chatbot needs is the amount of money to transfer from your account.  Be sure to include a dollar sign ("$") before the amount as shown in the screen shot.

Enter a value and click Send.

![<picture 2-3>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/2-3.jpg)
 

4.	Now let's try sending all three components in the initial message.
Enter and then send, Pay 25 euro to the babysitter from savings.

If you provide all the required bits of data all at once, the chatbot can process this and return a confirmation.
 
![<picture 2-4>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/2-4.jpg)
  
 
Try out some alternate phrasing, different accounts, and different amounts, like: 

- I’d like to send Sasha $20 for lunch.  	
- Pay Mom for rent on the 1st of every month using Visa.  
- Pay Lauren $15 for photos. 
- Send $500 to Mom from Savings every month.


In the next section, you will test out how Track Spending works.


**Step 3: Test the Track Spending intent**

In this section, you’ll see how the chatbot can return the amount of money that you spent from a specific category during a certain time frame.
Testing this intent requires a bit more precision. The way this function is set up, you need to know a couple of things: the spending category and a period of time to use as a measurement.

1.	 Inside the Tester, enter How much did I spend on gas? and then click Send.
The return response specifies the amount, the category and a time period.

![<picture 3-1>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/3-1.jpg)

2.	Click the Reset button. Next, enter How much did I spend at restaurants? and then click Send.
 
![<picture 3-2>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/3-2.jpg)

3.	Click Reset, enter another How much did I spend on travel? and then click Send.
 
![<picture 3-3>](https://github.com/cloud-is-coming/oraclecloud/blob/master/chatbot-get-started/lab1/3-3.jpg)


Similar to your earlier testing, try some other statements that specify a time frame and a category. Here are some that may help: 


- How much did I spend eating out last week?
- How much did I spend on clothes last month?
- How much did I spend on gas in October?
- How much did I spend on gas using my Visa cc last month?

In some cases, you will receive a message that you've spent $0 for a spending category. If you get this error, just refine your wording and try again.

Congratulations! You’ve completed the first chatbot lab. In subsequent labs, you'll learn how to design, build, and test the MasterBot that you just explored.

