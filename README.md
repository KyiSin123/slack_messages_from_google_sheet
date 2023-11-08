# How to send Slack messages from Google Sheet

1. Firstly, you need to have a slack account and a corresponding workspace. If not, sign up a Slack account and create a workspace.

2. Create a channel in your workspace and add your coworkers.

3. Create an app in this slack api site. https://api.slack.com/ <br>
   In this option <b> Pick a workspace to develop your app in: </b> Choose your created workspace.

4. Go your app => Features => Incoming Webhooks => Change <b>Activate Incoming Webhooks </b> from <b> Off </b> to <b> On </b>

![image](https://github.com/KyiSin123/slack_messages_from_google_sheet/assets/65592594/d49345bd-88a3-4e36-b802-9ef639e5d2d3)

5. After switching on, the following screen will be displayed. 

![image](https://github.com/KyiSin123/slack_messages_from_google_sheet/assets/65592594/e07154b0-29c9-4ba7-9f36-668b8e615a99)   

6. Click <b> Add New Webhook to Workspace </b> and the following screen will be appeared.

![image](https://github.com/KyiSin123/slack_messages_from_google_sheet/assets/65592594/ae167eb8-c0bc-4976-9639-c86f4e605f16)

7. Select the channel you want to send message and click <b> Allow </b>. Note the resulted webhook URL and we will use this later.
   
8. Create a google sheet and prepare data you want to send to slack.
   
9. Go Extensions => Apps Script
   
![image](https://github.com/KyiSin123/slack_messages_from_google_sheet/assets/65592594/2deaebe3-80d5-4264-a4fa-34ea27fc57f5)

10. Write script in script editor. Here is sample code.
```
function sendNotificationToSlack() {
  var url = "your_resulted_webhook_url"
  var sh = SpreadsheetApp.getActiveSpreadsheet()
  var sheetToSend = sh.getSheetByName("sample_sheet")
  var data = sheetToSend.getRange(2, 5).getValue()
  var params = {
    method: "post",
    contentType : "application/json",
    payload: JSON.stringify({      
      "text":data              //you can send any message you want to
    })
  }

  const sendMsg = UrlFetchApp.fetch(url, params)
  var respCode = sendMsg.getResponseCode()

  //these logs are optional to see the process works
  Logger.log(sendMsg)
  Logger.log(respCode)
```

11. Moreover, you can set timer according to the timing you want to send message. Click <b>clock</b> icon in apps script editor.

12. Click <b> Add Trigger </b> button and do setting as you want to.
    
![image](https://github.com/KyiSin123/slack_messages_from_google_sheet/assets/65592594/56e7b46f-c9c2-4851-ae8f-6b11813742d8) 

13. You can change your bot icon in Basic Information => Display Information

![image](https://github.com/KyiSin123/slack_messages_from_google_sheet/assets/65592594/cf37e110-dc50-4d75-ba32-6a7f1eaf1972)

