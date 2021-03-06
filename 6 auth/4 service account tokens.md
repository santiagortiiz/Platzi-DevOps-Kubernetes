# Service account tokens
- Exists in the kubernetes API
- Can be created, updated and deletes
- They are linked to the secrets
- They are used to grant permissions

# get the service account
- kubectl get serviceaccounts | kubectl get sa
- kubectl get sa default -o yaml
```
apiVersion: v1
kind: ServiceAccount
metadata:
  creationTimestamp: "2022-06-16T02:05:09Z"
  name: default
  namespace: default
  resourceVersion: "410"
  uid: e4c97716-8572-41d5-a02d-924212642e51
secrets:
- name: default-token-ttldp
```

# get the secret name
- kubectl get sa default -o json
```
{
    "apiVersion": "v1",
    "kind": "ServiceAccount",
    "metadata": {
        "creationTimestamp": "2022-06-16T02:05:09Z",
        "name": "default",
        "namespace": "default",
        "resourceVersion": "410",
        "uid": "e4c97716-8572-41d5-a02d-924212642e51"
    },
    "secrets": [
        {
            "name": "default-token-ttldp"
        }
    ]
}
```

# get the token of the secret
- kubectl get secret <secret_name>
- kubectl get secret default-token-ttldp -o yaml
```
apiVersion: v1
data:
  ca.crt: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURCakNDQWU2Z0F3SUJBZ0lCQVRBTkJna3Foa2lHOXcwQkFRc0ZBREFWTVJNd0VRWURWUVFERXdwdGFXNXAKYTNWaVpVTkJNQjRYRFRJeU1EWXhNREU0TVRjMU1sb1hEVE15TURZd09ERTRNVGMxTWxvd0ZURVRNQkVHQTFVRQpBeE1LYldsdWFXdDFZbVZEUVRDQ0FTSXdEUVlKS29aSWh2Y05BUUVCQlFBRGdnRVBBRENDQVFvQ2dnRUJBS05iCnBqYTdFMklEYkxmaFUyUmY4ZklJYnNsVDVJNFpFbjV2dVVab1pkSjNwbjhOZ1RSL09IbU95d2MrYjlBM1JmZXEKTnRySXdmM0FKT3N5bWdScDd0Z0lWRWZ4aHppcXE0Q0lBMHdDTFlkVWpiVkNrQkRKQi9DQm5YZXRoK1FPRk12cApIenR3VHpCU25nUnBCbXowN1pQancyUVNnNXlscHFoK29KdGhuelFBMG9zSDlGT0JWYUswbjdxSktqNGkzMGlnCk8xUXRLU1FYRjQvaDdLdEVNYWFaK1Z1bGpreDU1NkJRaEo4T1RjbVMySUtlQjBHWXB5NlhrSEJiTDBuWHg2OXYKK1grRkh4R01WdVlmM1hQR21rQUFlWkM4UWJOdE9WMVFzYkR2MDMzRjJyTDZiQ2h4eXNXdlg5RHZBMFdtR2RGagpFZUdBQjBJSUNkMGs0NTBVYUxFQ0F3RUFBYU5oTUY4d0RnWURWUjBQQVFIL0JBUURBZ0trTUIwR0ExVWRKUVFXCk1CUUdDQ3NHQVFVRkJ3TUNCZ2dyQmdFRkJRY0RBVEFQQmdOVkhSTUJBZjhFQlRBREFRSC9NQjBHQTFVZERnUVcKQkJUK0haZm9meExsQkM3c1loUy9TS2VIZ3pYbzJ6QU5CZ2txaGtpRzl3MEJBUXNGQUFPQ0FRRUFWWU5DOFJxOQprTFZsSStheW11emU5dlkxSlZEWW5ka3QwdGliTTBtVkNsYk8rRW9rTlIyWWVNVlFuak5NUlRoQ0pOWFFuVUpGCjVNR3lzVjBuL1cxS0NQdFdsMEh5NmMwOTdtaGxWMldFV0h0a0c4NlVIYmFsNktOYUhFZC9zMitxQVNCZkpIVFcKS1JlOXlyUXBHUk9qZW1aT2NjRm5DUnd1OC9Zc0lDMHlSNU5zSTFoVmpSSmRUa3UxNk55T0F6c2JBZ2Zpby84VwpqNFhEVlNQWkpmRHpuWGU5a2xwQUtCMGlrMnlWVDhUOHRoT2R3bjcvL1gzbkdyZTBhQnJrZUdUaGpQOER5YjUrCjVOT3Z2ZXlQVlZtSTFQNEFsQmlHaWs4YWFjMDVlT2d2dGdwWEFVOUo1bHVTL0ZHZjVNT2ZZcXJoZE1XWjFQVHEKWkQ1dGJVS2tpL3FNOUE9PQotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==
  namespace: ZGVmYXVsdA==
  token: ZXlKaGJHY2lPaUpTVXpJMU5pSXNJbXRwWkNJNklsUnJZekZNTmtzd01XeHBkVzgxZUdNM1QyOXhaa0ZXWTFNM2RFSTBlakJ3WTFwM2RqQkpNVTVGT1ZVaWZRLmV5SnBjM01pT2lKcmRXSmxjbTVsZEdWekwzTmxjblpwWTJWaFkyTnZkVzUwSWl3aWEzVmlaWEp1WlhSbGN5NXBieTl6WlhKMmFXTmxZV05qYjNWdWRDOXVZVzFsYzNCaFkyVWlPaUprWldaaGRXeDBJaXdpYTNWaVpYSnVaWFJsY3k1cGJ5OXpaWEoyYVdObFlXTmpiM1Z1ZEM5elpXTnlaWFF1Ym1GdFpTSTZJbVJsWm1GMWJIUXRkRzlyWlc0dGRIUnNaSEFpTENKcmRXSmxjbTVsZEdWekxtbHZMM05sY25acFkyVmhZMk52ZFc1MEwzTmxjblpwWTJVdFlXTmpiM1Z1ZEM1dVlXMWxJam9pWkdWbVlYVnNkQ0lzSW10MVltVnlibVYwWlhNdWFXOHZjMlZ5ZG1salpXRmpZMjkxYm5RdmMyVnlkbWxqWlMxaFkyTnZkVzUwTG5WcFpDSTZJbVUwWXprM056RTJMVGcxTnpJdE5ERmtOUzFoTURKa0xUa3lOREl4TWpZME1tVTFNU0lzSW5OMVlpSTZJbk41YzNSbGJUcHpaWEoyYVdObFlXTmpiM1Z1ZERwa1pXWmhkV3gwT21SbFptRjFiSFFpZlEuYTF0Uzk2TENlZ0J2SGQyRk1mbGR0blV4MWlaQ1dRUU5uQjM4UzdmWFBfZm1YVE9jLVMySjN3OWE0OXZXajY0NmN3VzFwTldDbElvN01HRmhSekxMbHRHc3RjdGJqZEJoS0ZJenk0czhrMEpPam45MEpNdFlncjJvM1g3ODlJclBRZDB0RW93SGRDeVJNb3FnQnItUlRuYmJMb1F5R3k4clAwbkdpdjVZUXlCS0lWNFp0ZHBQNzByNVcxc3ROR2VGcE8yUUhYVVpKNWUtN3NYU3FLSElCMzUxeG9KSDlUYndYSjhPOFpXYTU5dUJtc1hoWXZYUDEtNTZ3RGVUYV9tZkZkR1BHWFJmSGVzSVAzYjNqSFdocVRCSWMtaE5GWU5mNWxLbjY1dDc5TmdvdklraWZwcV9DbjQ4dzdGc3lnR3NrcWJ6NFNKQ3FtVWZvMk0zYWRyYkhn
kind: Secret
metadata:
  annotations:
    kubernetes.io/service-account.name: default
    kubernetes.io/service-account.uid: e4c97716-8572-41d5-a02d-924212642e51
  creationTimestamp: "2022-06-16T02:05:09Z"
  name: default-token-ttldp
  namespace: default
  resourceVersion: "408"
  uid: 2ae3a669-91ed-4a58-99bb-c8abf072fa7b
type: kubernetes.io/service-account-token
```

# decode the token
- kubectl get secret default-token-ttldp -o json | jq -r .data.token | base64 -d
```
eyJhbGciOiJSUzI1NiIsImtpZCI6IlRrYzFMNkswMWxpdW81eGM3T29xZkFWY1M3dEI0ejBwY1p3djBJMU5FOVUifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6ImRlZmF1bHQtdG9rZW4tdHRsZHAiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC5uYW1lIjoiZGVmYXVsdCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50LnVpZCI6ImU0Yzk3NzE2LTg1NzItNDFkNS1hMDJkLTkyNDIxMjY0MmU1MSIsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDpkZWZhdWx0OmRlZmF1bHQifQ.a1tS96LCegBvHd2FMfldtnUx1iZCWQQNnB38S7fXP_fmXTOc-S2J3w9a49vWj646cwW1pNWClIo7MGFhRzLLltGstctbjdBhKFIzy4s8k0JOjn90JMtYgr2o3X789IrPQd0tEowHdCyRMoqgBr-RTnbbLoQyGy8rP0nGiv5YQyBKIV4ZtdpP70r5W1stNGeFpO2QHXUZJ5e-7sXSqKHIB351xoJH9TbwXJ8O8ZWa59uBmsXhYvXP1-56wDeTa_mfFdGPGXRfHesIP3b3jHWhqTBIc-hNFYNf5lKn65t79NgovIkifpq_Cn48w7FsygGskqbz4SJCqmUfo2M3adrbHgbase64: invalid input
```

# hit the kubernetes-api with the decoded token (does not work)
- kubectl get svc -n default | grep kubernetes
- minikube ssh
- curl 10.96.0.1 -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6IlRrYzFMNkswMWxpdW81eGM3T29xZkFWY1M3dEI0ejBwY1p3djBJMU5FOVUifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6ImRlZmF1bHQtdG9rZW4tdHRsZHAiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC5uYW1lIjoiZGVmYXVsdCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50LnVpZCI6ImU0Yzk3NzE2LTg1NzItNDFkNS1hMDJkLTkyNDIxMjY0MmU1MSIsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDpkZWZhdWx0OmRlZmF1bHQifQ.a1tS96LCegBvHd2FMfldtnUx1iZCWQQNnB38S7fXP_fmXTOc-S2J3w9a49vWj646cwW1pNWClIo7MGFhRzLLltGstctbjdBhKFIzy4s8k0JOjn90JMtYgr2o3X789IrPQd0tEowHdCyRMoqgBr-RTnbbLoQyGy8rP0nGiv5YQyBKIV4ZtdpP70r5W1stNGeFpO2QHXUZJ5e-7sXSqKHIB351xoJH9TbwXJ8O8ZWa59uBmsXhYvXP1-56wDeTa_mfFdGPGXRfHesIP3b3jHWhqTBIc-hNFYNf5lKn65t79NgovIkifpq_Cn48w7FsygGskqbz4SJCqmUfo2M3adrbHgbase64"