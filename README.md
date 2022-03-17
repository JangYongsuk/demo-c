# demo-c

Demo C 코스
<BR>
<BR>
oc scale deploymentconfig app --replicas=2
<BR>
oc set resources dc app --requests='cpu=1000m,memory=1Gi' --limits='cpu=1000m,memory=1Gi'
<BR>
oc autoscale dc jws-app --min 2 --max 8 --cpu-percent=70 -n demo-b
