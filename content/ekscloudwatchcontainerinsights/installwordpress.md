---
title: "Install Wordpress"
chapter: false
weight: 2
---


![alt text](/images/ekscwci/wordpresslogo.png "Wordpress Logo")

We’ll be using the following Wordpress Distribution to install Wordpress to our EKS cluster. To install this we'll be using helm for an easy deployment method. 

https://github.com/helm/charts/tree/master/stable/wordpress 

In your Cloud9 Workspace terminal you just need to run the following command to deploy wordpress. 

```
helm install stable/wordpress 
```

You will see that this chart does a number of items. Including creating a persistent volume clain in EKS, create a Pod named after the release of Wordpress being installed (at time of this lab creation “understood-zebra” ) Multiple secrets stores and a stateful set. 
 

![alt text](/images/ekscwci/helminstalloutput.png "Helm Install Output")
 

Once your install is complete you will get an output like the below. This contains important information about how to connect to your Wordpress site. You will need to save your Loadbalancer URL for the load testing portion. 

{{% notice note %}}
**NOTES:**  
1. Get the WordPress URL:
  **NOTE:** It may take a few minutes for the LoadBalancer IP to be available.  
       Watch the status with: ```'kubectl get svc --namespace default -w understood-zebu-wordpress' ``` *(depending on time of install the Wordpress version can change)*

{{% /notice %}}
#### Getting your Load Balancer Url:

You’ll need the URL for your Wordpress site. This is easily accomplished by running the below from your terminal window. Copy and paste it from the output of your install of Wordpress. 

```
 export SERVICE_IP=$(kubectl get svc --namespace default understood-zebu-wordpress --template "{{ range (index .status.loadBalancer.ingress 0) }}{{.}}{{ end }}")
  echo "WordPress URL: http://$SERVICE_IP/"
  echo "WordPress Admin URL: http://$SERVICE_IP/admin"
```
Once ran you’ll get an output like below containing your site URL and Admin logon url. You will need both. 
 

![alt text](/images/ekscwci/lboutput.png "LB Output")
*Your LoadBalncer name will vary, so don’t use the one in the example.*

 
