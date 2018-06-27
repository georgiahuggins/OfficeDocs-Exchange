---
title: "Use a screen reader to trace an email message in the Exchange admin center"
ms.author: v-maleo
author: maggsl
ms.date: 12/9/2016
ms.audience: ITPro
ms.topic: article
ms.service: exchange-online
localization_priority: Normal
ms.custom: A11y_UseSR
ms.assetid: c95dd3ac-27e3-47ac-9130-5314a72ab4bd
description: "You can trace email messages by using your screen reader in the Exchange admin center (EAC) in Exchange Online. This is helpful if users are wondering whether their messages are delayed or possibly lost in delivery. With message tracing, you can follow messages as they pass through Exchange Online and determine whether a targeted email message was received, rejected, deferred, or delivered."
---

# Use a screen reader to trace an email message in the Exchange admin center

You can trace email messages by using your screen reader in the Exchange admin center (EAC) in Exchange Online. This is helpful if users are wondering whether their messages are delayed or possibly lost in delivery. With message tracing, you can follow messages as they pass through Exchange Online and determine whether a targeted email message was received, rejected, deferred, or delivered. 
  
## In this topic

- [Get started](use-screen-reader-to-trace-an-email-message-in-exchange-admin-center.md#BKMK_GetStarted)
    
- [Create a new message trace](use-screen-reader-to-trace-an-email-message-in-exchange-admin-center.md#BKMK_CreateMsgTrace)
    
- [Review the status of pending or completed message traces](use-screen-reader-to-trace-an-email-message-in-exchange-admin-center.md#BKMK_ReviewStatus)
    
## Get started
<a name="BKMK_GetStarted"> </a>

Navigate with Internet Explorer and keyboard shortcuts, and make sure that you have the appropriate Office 365 subscription and admin role to perform this task. Then, open the EAC and get started.
  
### Use your browser and keyboard to navigate in the EAC

Exchange Online, which includes the EAC, is a web-based application, so the keyboard shortcuts and navigation may be different from those in Exchange 2016. [Accessibility in the Exchange admin center](accessibility-in-exchange-admin-center.md).
  
For best results when working in the EAC in Exchange Online, use Internet Explorer as your browser. [Learn more about Internet Explorer keyboard shortcuts](https://go.microsoft.com/fwlink/?LinkID=787614).
  
Many tasks in the EAC require the use of pop-up windows so, in your browser, be sure to [enable pop-up windows for Office 365](https://go.microsoft.com/fwlink/?LinkID=317550).
  
### Confirm your Office 365 subscription plan

Exchange Online is included in Office 365 business and enterprise subscription plans, but capabilities may differ by plan. If your EAC doesn't include a function described in this article, your plan might not include it.
  
For more information about the Exchange Online capabilities in your subscription plan, go to [What Office 36 business product or license do I have?](https://go.microsoft.com/fwlink/?LinkID=797552) and [Exchange Online Service Description](https://go.microsoft.com/fwlink/?LinkID=797553).
  
### Open the EAC, and confirm your admin role

To trace a message, [Use a screen reader to open the Exchange admin center](use-screen-reader-to-open-exchange-admin-center.md) and check that your Office 365 global administrator has assigned you to the Organization Management, Compliance Management, and Help Desk admin role groups. Learn how to [Use a screen reader to identify your admin role in the Exchange admin center](use-screen-reader-to-identify-admin-role-in-exchange-admin-center.md).
  
## Create a new message trace
<a name="BKMK_CreateMsgTrace"> </a>

You might find that you need a message trace when a user contacts you about messages that are not delivered or are taking longer than usual to be delivered. You can trace a message using various criteria, including email address, date range, delivery status, and message ID.
  
1. In the EAC, press Ctrl+F6 until the primary navigation pane has the focus and you hear "Dashboard, Primary navigation link."
    
2. Tab to **mail flow**, and press Enter. 
    
3. To move to the menu bar, press Ctrl+F6. 
    
4. Tab to **message trace**. You hear "Message trace, Secondary navigation link." Press Enter. 
    
5. To access the main window list view, press Ctrl+F6. You hear "Message was sent or received combo box, Past 48 hours."
    
6. The **Date range** combo box has the focus, and the default setting is **Past 48 hours**. To cycle through the other choices, including **Past 24 hours,** **Past 7 Days**, and **Custom**, press the Up Arrow or Down Arrow key. 
    
    > [!TIP]
    > If you select **Custom**, you can tab to and enter the time zone, start date and time, and end date and time. These fields are not available unless you select **Custom** in the **Date range** combo box. Note that there might not be any data for messages that are less than four hours old. You cannot run a message trace on a message more than 90 days old. 
  
7. Tab to the **Delivery status** combo box. Choices are **All** (the default setting), **Delivered**, **Failed**, Pending, **Expanded**, **Quarantined**, **Filtered as spam**, and **Unknown**. Press the Down Arrow or Up Arrow key until the delivery status you want is selected. 
    
8. Tab to the **Message ID** text box. This is an optional field, but it can help narrow the search results. The Message ID or Client ID is generated by the sending system and can be found in the header of the message with the **Message-ID**: token. The Message ID might include angle brackets (\< \>). 
    
9. To specify senders (one or more) in the message trace, tab to the **add sender** button and press Enter. In the **Select Members** dialog box, the **Search** button has the focus. 
    
1. To search for a user within your organization, press Enter, type all or part of the name of the user, and then press Enter.
    
2. Press the Tab key about seven times until you hear the name of the user in the search results list. 
    
3. To add the user to the list of senders for the message trace, press the Down Arrow key until you hear the user's name and then press Enter. The list of users retains the focus, so you can continue to add more users by selecting their mailboxes and pressing Enter.
    
    > [!TIP]
    > To check the users you've added, tab to the **Add** button. To hear the list of users, press the Tab key again. The first name is read. To hear the second name in the list, press the Tab key one more time. Continue pressing the Tab key until you hear the names of all the users you've added. To delete a user from the list, activate the **Remove** link by pressing Enter when you hear the user name. 
  
4. To specify an external user or an email address with a wildcard (for example, \*@contoso.com), press the Tab key until you hear "Check names edit, Type in text." (In Narrator, you hear "Editing.") Type the email address of the external user or the address with a wildcard. To select the **Check names** button, press Shift+Tab and then press Enter. This verifies the email address and adds it to the list of users. 
    
    > [!TIP]
    >  When you specify a wildcard, you cannot also add full email addresses to the message trace. >  Be aware that if you type an external email address and press Enter, this adds the user to the list and then closes the dialog box. If you're not finished, use the **Check names** button to add it instead. 
  
5. When you finish adding users, tab to the **OK** button and press Enter. The ** message trace ** page has the focus again, and the **Sender** text box lists the senders you specified for the message trace. 
    
10. To add a recipient to the message trace instead of or in addition to the senders, tab to the **add recipient** button and press Enter. In the **Select Members** dialog box, the **Search** button has the focus. To add one or more recipients to the message trace, repeat step 9. 
    
11. On the **message trace** page, tab to the **search** button and press Enter. The **Message Trace Results** page opens and shows the date, sender, recipient, subject, and status of the message(s) that are a result of the message trace. 
    
    > [!TIP]
    > When you run a trace for messages that are less than seven days old, the messages should appear within 5-30 minutes. When you run a message trace for messages that are more than seven days old, results may take up to a few hours. So if the **Message Trace Results** page appears empty at first, check again later. An easy way to do this is to keep this page open, and, on the toolbar, periodically tab to the **Refresh** button and then press Enter. 
  
12. To close the **Message Trace Results** page, tab to the Close button and press Enter. 
    
## Review the status of pending or completed message traces
<a name="BKMK_ReviewStatus"> </a>

It might take a few minutes to a few hours for message trace results to return. You can check the status of pending or completed message traces.
  
1. In the EAC, press Ctrl+F6 until the primary navigation pane has the focus and you hear "Dashboard, Primary navigation link."
    
2. Tab to **mail flow**, and press Enter. 
    
3. To move to the menu bar, press Ctrl+F6. 
    
4. Tab to **message trace**. You hear "Message trace, Secondary navigation link." Press Enter. 
    
5. To access the main window list view, press Ctrl+F6. You hear "Message was sent or received combo box." 
    
6. The **Date range** combo box has the focus. To move to the View **pending or completed traces** link, press Shift+Tab. Press Enter. The **pending or completed traces** page opens and shows the report title, date submitted, report status, and messages. 
    
7. To refresh the page, make sure that the **Refresh** button has the focus (this is the default setting) and then press Enter. 
    
8. To close the **pending or completed traces** page, tab to the **Close** button and press Enter. 
    
> [!NOTE]
> For more information, refer to [Run a Message Trace and View Results](https://go.microsoft.com/fwlink/?LinkId=799440). 
  
