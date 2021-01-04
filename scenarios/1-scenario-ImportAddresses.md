# Import addresses

This example shows how to import addresses into the system. It is a shell script which shows how to add a list of customers to a job.

```
LINK to API docs: https://<YOUR_SITE_NAME>.telemagic.no:8894/rest/#1316391243
```

It is a two-step process:

1. Initial request which uploads the list of addresses
1. Second request to check whether the upload was successful.

The reason it is done this way, is that you might upload very many addresses which the server needs time to process, imagine thousands of addresses.

TMG will start an upload job in the background with the addresses provided in the body. A 200 response on 1) tells the job was started successfully, not whether it is able to import successfully. In order to check whether the upload is a success or not, you need to check the status of the upload job in 2).


```
#!/usr/bin/env bash

echo 'Sending to TMG, note the upload report ID in the response'

SITE_NAME=tmg_site_name
PROJECT_NAME=the_project_name_in_tmg
JOB_NAME=the_job_name_in_tmg

USER_NAME=your_tmg_user_name
PASSWORD=your_tmg_password


# 1) upload the addresses
UPLOAD_REPORT_ID=`curl -u $USER_NAME:$PASSWORD -X POST  https://$SITE_NAME.telemagic.no:8894/rest/addresslist/project/$PROJECT_NAME/job/$JOB_NAME/json \
-H 'Content-Type: application/json' \
-d @example_body_with_one_customer.json`

echo
echo 'Using the upload report ID below, to check whether the upload was successful'
echo 'You might need to retry this if you uploaded many addresses. Here we sleep 1 sec, to be sure it is done'
sleep 1

# 2) check whether the upload was a success
curl -u $USER_NAME:$PASSWORD https://$SITE_NAME.telemagic.no:8894/rest/addresslist/report/$UPLOAD_REPORT_ID/ \
-H 'Content-Type: application/json'

```

Below is the contents of the file *example_body_with_one_customer.json*.


```
[
   {
      "customerField":{
         "ticket":"abc123",
         "whatever":"something or anything"
      },
      "phoneNo":"+4712312",
      "country":"Norway",
      "name":"Ola",
      "eMail":"ola@nordmann.com",
      "lastName":"Nordmann",
      "address":"South street 1",
      "zip":"1234",
      "city":"City name",
      "company":"Green Company",
      "companyContact":"Kontact K",
      "companySector":"Sector S",
      "customerId":"some-ext-id-1",
      "gender":"Male",
      "customerNote":"customer note 1",
      "sessionNote":"session note 1"
   }
]
```


In order to check whether the upload is a success or not, you need to check the status of the upload job, see 2). Example response can be like this, in case there was a failure:


```
{
   "id":1399,
   "project":"x",
   "job":"y",
   "duplicate":[

   ],
   "error":{
      "id":3922,
      "uploadId":1399,
      "entryCount":1,
      "result":"error",
      "duplicateProject":null,
      "duplicateJob":null,
      "contentType":"json"
   },
   "created":"2018-02-15T07:39:18.000+0000",
   "uploadedBy":"ApiCalls",
   "state":"completed"
}
```

Note that phoneNo is required, the rest can be omitted. The fields inside *customerField* can be whatever you want, they are custom. When you design how the customer card should look, you can refer to these field names – and they will show up with the values you imported.

##### Postman Examples
    Go to: collection > addresslist > POST Import addresses
