# Aviatrix- AWS Gateway Single AZ HA

## Description

AWS supports cloudwatch alarm actions, which can be associated with any instance to automatically recover from system/instance failure by rebooting the instance.
In this guide we will show how to attach cloudwatch alarm option to recover an unreachable Aviatrix gateway,which will ensure gateway HA within an Availability Zone.

This can be done from cloudformation template or manually from AWS console.

### Option1: Using Cloudformation template

1. Download this repository as zip file, by clicking on top right green button named `Clone or download`, and then click on `Download ZIP`.

2. Extract the downloaded zipped file on your local system. You will get a directory named `Aviatrix-Gateway-Recovery-master`. Inside this directory, there will be a file named `aviatrix-gateway-recovery.json`.

3. Now go to `AWS Console`-> `Services` -> `Management Tools`-> `CloudFormation`. Click `Create stack`.

4. On the next screen, Select `Upload a template to Amazon S3`. Click on `Choose file`, and then select `aviatrix-gateway-recovery.json` from directory `Aviatrix-Gateway-Recovery-master` created in Step 2.

5. Click next. On the Stack Name textbox, Name your Stack -> Something like *GatewayRecovery*. Select Gateway instance for which you want to enable recovery. Click `Next`.

6. Specify your options/tags/permissions as per your policies, when in doubt just click `Next`. Review all configurations and click `Create`.

7. Wait for status to change to `CREATE_COMPLETE`. If fails, debug or contact Aviatrix support.

### Option2: Manually from AWS console

Alternatively, you can manually enable cloudwatch alarm action directly from AWS console.

1. Login to AWS Console, and select `Instances`. Make sure you are in the correct region. Select your gateway instance for which you want to enable recovery. 

2. Click `Actions`-> `CloudWatch Monitoring`-> `Add/Edit Alarms`-> `Create Alarm`. Uncheck `Send a notification to`. Check `Take the action` and check `Reboot the instance`. Check `Create IAM role: EC2ActionsAccess`, if appears. In `Whenever` select `Minimum` of `Status Check Failed (Any)`. Update `For at least` to `5`, `consecutive period(s) of` to `1 minute`.

3. Click `Create Alarm`. You should get a popup `Alarm Created Successfully.`
