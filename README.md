# Start an application on the DSRI (workshop)

A workshop to get started with the **Data Science Research Infrastructure (DSRI)** in an hour 🕐 (hopefully)!

During this workshop, you will:

* Access the Data Science Research Infrastructure web UI
* Create a new application from a template in the catalog (RStudio, JupyterLab or VScode )
* Access the application
* Add source code and data in the application

Prerequisites:

* A web browser (Chrome preferably, as some other web browsers have issues with the VSCode terminal)
* An account on the DSRI with your UM email
* Access to the UM VPN, or direct connection to UMnet or eduroam at Maastricht University

---

## Access the DSRI

1. Connect to the VPN

	- Students can use the Student Desktop (athenadesktop.maastrichtuniversity.nl)

2. Access the DSRI 

	- https://maastrichtu-ids.github.io/dsri-documentation/docs/access-dsri  

3. 👩‍💻 Go to the [**workshops** project](https://app.dsri.unimaas.nl:8443/console/project/workshops/overview) in the OpenShift web UI

---

## Start an application

Start a **JupyterLab/RStudio/VSCode** application from the DSRI catalog in ids-projects

📖 See the documentation at https://maastrichtu-ids.github.io/dsri-documentation/docs/deploy-from-template 

1. 👩‍💻 Use your name to generate a unique **Application name**, e.g. `rstudio-vemonet`
2. Use this storage claim name: **pvc-mapr-workshops** 
	- It can be found at https://app.dsri.unimaas.nl:8443/console/project/workshops/browse/storage
	- ⚠️ When copy/pasting the storage name it can happen that a space is added at the end. **Be careful to trim all spaces at the start and the end of the storage name** before starting the application, otherwise it will fail

2. Use your application name as **Storage folder**

3. Access the application you just started

	- 👩‍💻 You can find the URL of your application in the OpenShift web UI **workshops** overview

---

## Upload your code

We recommend you to use `git`, you can use directly from the commandline in all applications, or use the web UI integration each app proposes.

See the documentation for each application:

* RStudio: https://maastrichtu-ids.github.io/dsri-documentation/docs/deploy-rstudio#use-git-in-rstudio
* VSCode: https://maastrichtu-ids.github.io/dsri-documentation/docs/deploy-vscode#use-git-in-vscode
* JupyterLab (with `jupyterlab-git` extension installed): https://maastrichtu-ids.github.io/dsri-documentation/docs/deploy-jupyter#use-git-in-jupyterlab

---

## Upload data

For small and medium size files: you can drag and drop in the application web UI, or use the **Upload files** button in RStudio.

For large data files you will need to install and use the `oc` command line interface.

> If you have the time it can be quickly installed on MacOS, Linux (works with WSL):
>
> * On **Linux**:
>
> ```bash
> wget https://github.com/openshift/origin/releases/download/v3.11.0/openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit.tar.gz
> tar xvf openshift-origin-client-tools*.tar.gz
> cd openshift-origin-client*/
> sudo mv oc kubectl /usr/local/bin/
> ```
>
> * On **Mac**:
>
> ```bash
> brew install openshift-cli
> ```
>
> * On **Windows** [checkout the documentation](https://maastrichtu-ids.github.io/dsri-documentation/docs/openshift-install#on-windows).

📖 See the complete documentation to upload data at https://maastrichtu-ids.github.io/dsri-documentation/docs/openshift-load-data 

---

## Stop and delete your application

👨‍💻 Stop your application from the OpenShift web UI **Overview** page:

![Stop your application](https://raw.githubusercontent.com/MaastrichtU-IDS/dsri-documentation/master/website/static/img/screenshot_scaledown_pod.png)

> Note: creating more than one pod ("Scale up") is useless for most data science applications, such as RStudio, VSCode or JupyterLab. It is only relevant for applications running as a cluster, like Apache Flink or Apache Spark.

👩‍💻 Delete your application:

* If you installed the `oc` command line interface, it is easier to use it to delete all the objects related to the applications:

```bash
oc delete all,secret,configmaps,serviceaccount,rolebinding --selector app=my-application
```

> Replace `my-application` by the Application name you defined.

* Otherwise you will need to manually delete a few objects related to your application in the OpenShift web UI:
  1. Delete the **Route**
  2. Delete the **Service**
  3. Delete the **Deployment Config** 

<img src="https://raw.githubusercontent.com/MaastrichtU-IDS/dsri-documentation/master/website/static/img/screenshot_delete_application.png" alt="Delete application from the web UI" style="max-width: 100%; max-height: 100%;" />

📖 See the complete documentation to delete an application at https://maastrichtu-ids.github.io/dsri-documentation/docs/openshift-delete-services#delete-an-application

---

## See you soon!

Fill this form to create a project on a longer term on the DSRI: 