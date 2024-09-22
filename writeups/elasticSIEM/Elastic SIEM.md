# TUTORIAL
-> Create an Elastic Account at [https://www.elastic.co/](https://www.elastic.co/)
-> Click on create new deployment
![[create_deployment.jpg]]

-> Set desired deployment settings according to your need. Make sure to understand what each option means, and how it might benefit your requirements. These are my settings:
![[deployment_settings.jpg]]

-> Click on Create Deployment, and on the next screen make sure to download the credentials or store it in a safe place
![[save_deployment_credentials.jpg]]

-> Click on continue once the deployment is created.
-> On the home page, click on the side-menu on the left and click on add integrations.
![[add_integrations.jpg]]

-> Search and choose elastic defend, and click add Elastic Defend on the next page
![[elastic_defend.jpg]]

-> Configure the integration, I will be using Complete EDR, choose whatever suits you. Click on save and continue
![[config_integration.jpg]]

-> When prompted, click on Install Elastic Agent (Note: the prompt appears at the bottom of the screen)
![[install_prompt.jpg]]

-> Choose your host type and copy the instructions and run them on your host machine
![[install_page.jpg]]

-> If successful, you should get the following output:
![[enroll_confirm.jpg]]

-> On the left hand sidemenu, under Observability, click on logs, and click on Stream (note: Explorer will replace Stream sometime in the future)
![[logs.jpg]]

-> Let's generate some logs so that we can query it on this screen and see if everything is working
-> Use nmap on your host machine `nmap -F 127.0.0.1` (you can run 3-4 nmap commands)
-> Use the following query to see all nmap related events: 
`process.args: "nmap"`
![[query.jpg]]

You should see some entries, hover over an entry and clock on the 3 dots -> view details and explore the log messages.

Now let's create a dashboard
-> On the left hand menubar, under Security, click on dashboards
-> Click on Create Dashboard on the top right
-> Click on Create Visualization
-> On the right, set how you would like your visualization to look, I have chosen area. Set horizontal axis to timestamp, and vertical to count. These are my final settings:
![[visual_settings.jpg]]

You will see a visual on the left showing you what your current settings will look like, you can see in the image attached, there is a spike, this spike is our set of nmap commands we ran earlier.

-> Click on Save and return, and then Save again and name your dashboard and give it a description. We have successfully created a dashboard

Let us now create an alert.

-> Under the same Security section, click on Alert (should be on the left)
-> Click on manage rules and clic on Create new Rule
-> Under Define Rule, select Custom Query
-> Enter the same query we entered earlier `process.args: "nmap"`
-> Click on Continue
-> Under About rule, set your name, description, severity, and risk score. These are my settings:
![[kali_alert.jpg]]

-> Click on Continue
-> Schedule the rule according to your needs, I will leave it at default
-> For Rule Actions, you can connect it to Jira, have it send you an email, send a Slack message, notify you on ms teams, etc. I will leave it blank for now, and click on Create & enable rule

We have successfully created an alert. To test that this works, run an nmap command on your host, and wait sometime for the alert to pick it up. I will run the nmap a few times.

![[alerts.jpg]]

As you can see, our alert has triggered 10 events, it is functioning correctly

To summarize, in this project, we've built a SIEM on elastic on a free trial account. We setup a deployment, added an integration for Elastic Defend, added a host to this integration with elastic client. We then queried our logs to see activity on nmap. Following that, we set up a dashboard with a visualization, and created an alert system that alerts whenever nmap is run.

Here is an alert created by malicious behaviour:
![[kali_malware_alert.png]]