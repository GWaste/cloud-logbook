
# Cloud Logbook

## Contents
- [Gwaste Architecture](#gwaste-architecture)
- [Cloud Storage](#cloud-storage)
- [AI Platform](#ai-platform)
- [App Engine](#app-engine)
- [Cloud Functions](#app-engine)

## Gwaste Architecture
![image](https://drive.google.com/uc?export=view&id=1pewrx5tOYPKZOAJ9ZhDVpuSTrQovqc-S)

## Cloud Storage
In our project we use Cloud Shell to create two buckets:
 1. To create the first bucket:   
   ```console
   $ gsutil mb gs://[OUR-PROJECT-ID]
   ```
 2. The second bucket:
   ```console
   $ gsutil mb gs://[OUR-PROJECT-ID]-tf2-models
   ```

 
## AI Platform
We use AI Platform (Models) to deploy our model in GCP.

The steps to deploy the model to the AI Platform is:
 1. Click Navigation Menu -> AI Platform
 2. Select Models
 3. Click [+] New Models button.
 4. Fill the name model as 'waste', then select the region, after that click Create
 5. Return to Models menu, click 'waste' model.
 6. Click [+] New Version button.
 7. Fill the version name as 'v1', and fill the Pre-built container settings with:
   ![image](https://drive.google.com/uc?export=view&id=1dG67prvVSTopJ247cyhAQdfM8pbN3d_H)
 8. Click Save and wait until versioning done.

## App Engine
With App Engine (Standard) we deploy the [web](https://cosmic-quarter-312712.et.r.appspot.com/) version of our product.

The steps to deploy is:
 1. Open Cloud Shell, then type commands below:
   ```console
   $ mkdir wep-app
   $ cd wep-app
   $ git clone https://github.com/HiWaste/web-app.git
   $ cd wep-app
   ```
   
2. Create two files: app.yaml and main.py, using commands:
   ```console
   $ sudo touch app.yaml
   $ sudo touch main.py
   ```
   Fill the app.yaml with this and main.py with this.
   
3. In root project:
    ```console
   $ cd hiwaste_web
   $ sudo vim settings.py
   ```
4. In settings.py, search ALLOWED_HOST = [], then chage as:
   ```console
   ALLOWED_HOST = ["*"]
   ```
   Save settings.py.
   
5. Return to root project: 
   ```console
   $ cd ..
   ```
6.  Test the web before deploy, with steps:
   ```console
   $ virtualenv env
   $ source env/bin/activate
   $ pip install -r requirements.txt
   ```
   Wait until the dependencies is installed, then type:
   ```console
   $ python3 manage.py runserver
   ```
    Click web preview on Cloud Shell, change port with: 8000, then  click Change and Preview. If the web running as well it's time to deploy!

7. Deploy time!
   Press Ctrl + C to stop web preview and then type:
    ```console
   $ gcloud app deploy
   ```
   And select the region and wait until done.
8. Result: https://cosmic-quarter-312712.et.r.appspot.com/product/3