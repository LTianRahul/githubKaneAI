# githubKaneAI

Create a AUTH details in your repo.
Follow the below instructions to create a secrets for your LT Username and AccessKey

Step 1: Go to your **existing Repo** and click on **Settings** (attached screenshot for your reference here)
<img width="1034" alt="image" src="https://github.com/user-attachments/assets/fc95aec1-1295-40c2-874d-4e8700fdc4b3" />

Step 2: Under **Settings**, Click on **Secrets and Variables** (attached screenshot for your reference here)
<img width="750" alt="image" src="https://github.com/user-attachments/assets/8ed2e281-cde9-4dcb-9f03-644add4add60" />

Step 3: Click on **Actions** (attached screenshot for your reference here)
<img width="1125" alt="image" src="https://github.com/user-attachments/assets/4d3ffc60-12fd-4f3a-a78b-2fb02b772c0f" />

Step 4: Click on **New repository secret** (attached screenshot for your reference here)
<img width="837" alt="image" src="https://github.com/user-attachments/assets/99606fdd-3488-4552-bce5-b3a87a6a03a2" />

Step 5: Enter **secret name** and get the credentials value in base64 from **postman** or can create it using any public website (update the info in the way i have showcased in screenshots) and Click on Add secret button

Screenshot from **postman** - <img width="1294" alt="image" src="https://github.com/user-attachments/assets/28aec5c2-5994-4248-b005-5708194d5e58" />

Screenshot from **GitHub** <img width="860" alt="image" src="https://github.com/user-attachments/assets/3ec44589-e1e1-45a6-8e4f-b0f18a17c5a0" />

Step 6: Go to **Actions** and then click on **New Workflow** (attached screenshot for your reference here)
<img width="1659" alt="image" src="https://github.com/user-attachments/assets/c8b5b2c3-c3af-498a-a935-898d63e97010" />

Step 7: Click on **Configure** for **Simple workflow**
<img width="1298" alt="image" src="https://github.com/user-attachments/assets/cabcdcc8-9c7b-4d3f-86c9-677cd62aef83" />

Step 8: Copy paste the below in file 

--------------------------------------------------------

```
name: KaneAI cURL Command

on:
  workflow_dispatch:
    inputs:
      test_run_id:
        description: 'The Test Run ID'
        required: true
        default: 'YOUR_TEST_RUN_ID'
      concurrency:
        description: 'Concurrency Level'
        required: false
        default: 1
      title:
        description: 'Unique Build Name'
        required: false
        default: 'UNIQUE_BUILD_NAME'
      region:
        description: 'Desired Region'
        required: true
        default: 'eastus'

jobs:
  run-curl:
    runs-on: ubuntu-latest
    steps:
      - name: Run Parameterized cURL Command
        run: |
          curl --location 'https://test-manager-api.lambdatest.com/api/atm/v1/hyperexecute' \
          --header 'Content-Type: application/json' \
          --header "Authorization: ${{ secrets.LT_Creds }}" \
          --data "{
              \"test_run_id\": \"${{ github.event.inputs.test_run_id }}\",
              \"concurrency\": ${{ github.event.inputs.concurrency }},
              \"title\": \"${{ github.event.inputs.title }}\",
              \"region\": \"${{ github.event.inputs.region }}\"
          }"

```
------------------------------------------------------


Edit the **details** as follows 

${{ secrets.AUTH_HEADER }}  to ${{ secrets.LT_Creds }}

default: 'YOUR_TEST_RUN_ID' to the Test Run value which you get from the Test Run dashboard section

Update as the informations as suggested above and then to run it go to the **Actions** page again

--------------------------- **To Run the workflow **---------------------------

Follow the Instructions and then click on **Run workflow**
<img width="1672" alt="image" src="https://github.com/user-attachments/assets/87eaa246-9d8e-47ce-871b-62b8110d0a6d" />

Enter the **The Test Run ID** value which you will get getting from the Test Run Dashaord, followed by Concurrency and other details and then click on **Run workflow** button
<img width="340" alt="image" src="https://github.com/user-attachments/assets/a78fd916-cc41-4527-893b-f73aa4f5ba78" />

**Whoooo**!!!! You did it... you should be able to see session up and running in your dashbaord with the yml output like this (refer the screenshot below)

<img width="1294" alt="image" src="https://github.com/user-attachments/assets/88e70555-39ad-4753-b54e-b7eb8225b99e" />




