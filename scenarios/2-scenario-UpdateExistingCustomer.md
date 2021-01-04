# Update Existing Customer

This example shows how to update an existing customer.

### Step 1: First you must find your customer

**IF you already have your TMG ID or project/job + customerId 
combination you can skip this step**

Use the customer search API to search for the 
customer: https://<yoursite>.telemagic.no:8894/rest/#-2014340205  

##### Postman Example
    Go to: collection > sales or customers > GET Find a specific customer by searching

### Step 2: Get current customer card data (OPTIONAL)

**This step is optional.** 

To get the customer sales data you will need to use this API:

    https://<yoursite>telemagic.no:8894/rest/#1443991229

If you need to know what data is currently set on the
customer before updating the customer. 

**NB: note that each order is returned with a number starting with 0**

##### Postman Examples
    Go to: collection > sales or customers > GET Get data on specific customer using TMG ID
    Go to: collection > sales or customers > GET Get data on specific customer using customerId

### Step 3: Update customer data

To put the customer sales data, you will need to use this API:

    https://<yoursite>telemagic.no:8894/rest/#420588881 

You only need to put the field you want to update or update on the
existing customer. 

##### Postman Examples
    Go to: collection > sales or customers > PUT Update existing customer using TMG ID
    Go to: collection > sales or customers > PUT Update existing customer using customerId



