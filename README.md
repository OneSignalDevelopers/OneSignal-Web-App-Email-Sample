# Web-App-Email-Sample

This is a sample web application to demostrate the usage of OneSignal and SendGrid. 

Emails can be used in a variety of ways. When we create an application is very important to make the user feel that the experience is being personalized and not just general for everyone. [OneSignal](https://onesignal.com) can help us with that. 

OneSignal has several tools in their one-stop dashboard that can help you increase your user experience. Some of those tools are Segments and Emails powered by [SendGrid](https://sendgrid.com/) by Twilio.

Thanks to [Segments](https://documentation.onesignal.com/docs/segmentation/), we can target a specific audience to send the emails to. For example the subscribers of your application or people that like certain topics of your blog.

Notes:
* Create a FREE [OneSignal](https://onesignal.com/) account 
* Follow the steps of the  [Typical setup](https://documentation.onesignal.com/docs/web-push-typical-setup)

## Sending User Emails To OneSignal

After following the steps for a Typical site setup, go back to your app, in the *index.html* file we are going to modify a bit our JavaScript code. 

At the bottom of your **script** tag, we are going to create a function called `setEmail()`. Inside of that function, we will trigger a prompt to ask the user for their email address. Finally, inside of that function, we will use the `setEmail()`  [method](https://documentation.onesignal.com/docs/email-quickstart) of the OneSignal SDK to assign the email address you entered in the prompt to the current user of the app.

If you look closely at the code below, you will notice that we are also using `OneSignal.sendTag()`

Tags can help you add information to the profile of a user. In our case, we are adding the user_name but you can add whatever information you want and as many tags as you need. Tags can also be used to segment users. For example, you can have a tag `country: USA` to use it to segment users per country and create marketing campaigns for users that only belong to the USA.

To learn more about tags, visit our [documentation](https://documentation.onesignal.com/docs/add-user-data-tags).

```javascript
function setEmail() {
            const email = prompt("Please enter your email", "example@domain.com");
            if(email !== null) {
                OneSignal.push(function() {
                OneSignal.setEmail(email).then(function(emailId) {
                    // Callback called when email have finished sending
                        console.log("emailId: ", emailId);
                        /*Creating a user_name identifier tag to be used in the email
                            Example: OneSignal.sendTag("user_name", "devpato");   
                        */
                        OneSignal.sendTag("user_name", "a_user_name");   
                    }); 
                });
                
            }
        }

```

Now, inside of your body tag, create a button that calls the `setEmail()` function.

```html
<body>
    <button onclick="setEmail()">Set Email</button>
</body>
```
