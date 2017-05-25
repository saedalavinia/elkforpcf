# Configuring PCF to Forward Application Logs to your ELK  
*** 

### Setting up the Project: 

##### Prerequisites: 
You need to have an ELK Stack and know the following information: 
* The URL and Port Numeber at which Logstash consumes Logs. For example:
syslog://ip_address:5000/
* The Username and Password for your Kibana Web Application. 

If you wish to deploy an instance of Logstash in AWS, ami-40e3a356 (US-EAST-1) is available and setup to consume logs as syslog://ip_address:5000/ and Kibana is configured with Username: kibanaadmin and Password: mypass. 
Email me at saedalav@gmail.com to gain access to this AMI as it is currently Private. 

This guide assumes that you have two application for which you would like to forward logs to your ELK Stack: 
- addressapi
- addressapiclient
And that Logstash is configured to consume logs at:
syslog://elk.alavinia.me:5000/ 


1. Execute the following commands: 

```sh 
cf login -a URL -u USERNAME -p PASSWORD
cf cups logstash-drain -l syslog://elk.alavinia.me:5000/
cf bind-service addressapi logstash-drain
cf bind-service addressapiclient logstash-drain
cf restage addressapi
cf restage addressapiclient