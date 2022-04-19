# demo-c

Auto Scaling
<BR>

<b>어플리케이션 생성</b>
<BR>
http://gitlab.ocp.demo.com/test/demo-c.git
<BR>
oc scale deploymentconfig app --replicas=2

<b>Auto Scaling</b>
<BR>
oc set resources dc app --requests='cpu=1000m,memory=1Gi' --limits='cpu=2000m,memory=2Gi'
<BR>
oc autoscale dc app --min 2 --max 8 --cpu-percent=50 -n demo-c
<BR>
watch -n 1 "oc get hpa app -n demo-c"
<BR>
watch -n 1 "oc adm top pod -n demo-c"
<BR>
watch -n 1 "oc get pod | grep Running"

<BR>
<b>부하생성</b>
<BR>
dd if=/dev/zero of=/dev/null
<BR>
<BR>
ab -n 30000 -c 300 http://app-demo-c.apps.ocp.demo.com/load.jsp

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
    
