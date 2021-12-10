### Introduction

When there are updated deployment (e.g. version 1 to version 2),  customer wants to release the latest version progressively. For example,  10% to version 2 and the remaining 90% to version 1.  This is called the A/B deployment.  There are 2 approaches to do it in openshift.   

### A/B deployment 

* Open Terminal tab.  
```execute
oc project service-sit-%username%
```

* Execute the command below.  To deploy another submitrequest with background as lightblue. 
```execute
oc new-app --name=submitrequest-blue  --image-stream='submitrequest:sit' -e COLOR=lightblue -e ENDPOINT=http://submitrequest-blue-service-sit-%username%.apps.cluster-2e68.2e68.sandbox1783.opentlc.com/ -e HOSTNAME=workshop-main.service-sit-%username%.svc.cluster.local
```

* Approach 1: To replace the service in existing route.  
```
oc patch route/submitrequest-white -p '{"spec":{"to":{"name":"submitrequest-blue"}}}'
```

* Approach 2: To assign certain workload to old and new version.  This is to assign 50%-50% load balancing.
```
oc set route-backends submitrequest-white submitrequest-white=1 submitrequest-blue=1
```

* Open console tab. Switch to `service-sit-%username% project.  

* Go to `Networking` -> `Routes`.   Right-click on `Locations` of `submitrequest-white` and select ` Open Link in Incognito Window`.  Do this several times and you will see the background is switching between white and blue. 


### Summary
In this lab, you have learned to use Route for A/B deployment.



