# demo-c

Auto Scaling
<BR>
<BR>
oc scale deploymentconfig app --replicas=2
<BR>
oc set resources dc app --requests='cpu=1000m,memory=1Gi' --limits='cpu=1000m,memory=1Gi'
<BR>
oc autoscale dc app --min 2 --max 8 --cpu-percent=50 -n demo-c
<BR>
oc get hpa app -n demo-c
<BR>
oc adm top pod -n demo-c

<BR>
dd if=/dev/zero of=/dev/null
<BR>
<BR>
ab -n 100 -c 10 http://app-demo-c.apps.ocp.demo.com/oom.jsp

<BR>
apiVersion: v1
kind: ResourceQuota
metadata:
  name: demo-quota
  namespace: demo-quota
spec:
  hard:
    limits.cpu: '4'
    limits.memory: 4Gi
    requests.cpu: '4'
    requests.memory: 4Gi
  scopes:
    - NotTerminating
    
