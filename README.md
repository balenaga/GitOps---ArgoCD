# GitOps---ArgoCD
## GitOps Principles ##
GitOps is a framework where the entire code delivery process is controlled by via Git,which also includes infra and application definitions as code and automation to deploy changes and rollbacks.Gitops can be considered as a extension of Infrastructure as a code that uses git as the version control system.
- Infra and application code must be declared in a decalrative state.
- All the declarative files also known as the desired state are stored in a git repository.
- GitOps operator,also known as software agent,automatically pull the desied state from Git and apply it in one or more environments or clusters.The GitOps operator can run in one of the clusters and can make or push changes to other clusters as well.
- The final principle is Reconciliation.The GitOps operator also make sure that the entire sysytem is self-healing to reduce the risk of human-errors the operator continuously loops through 3 steps
    - Observe (checks the repo for any changes in the desired state)
    - Diff (compared the resources received from the previous step to the actual state of the cluster)
    - Act (it uses a reconciliation function and tries to match the actual state to the desired state)
- ArgoCD installation \
Refer thise link https://argo-cd.readthedocs.io/en/stable/ \
kubectl create namespace argocd\
kubectl apply -n argocd --server-side --force-conflicts -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
- ArgoCD Architecture
<img width="743" height="708" alt="image" src="https://github.com/user-attachments/assets/b1480fe6-d9ce-44bb-9fc4-2d3385689bd2" />

- To check the pods after Argo CD installtion\
kubectl get pods -n argocd -w\
<img width="1875" height="951" alt="image" src="https://github.com/user-attachments/assets/83d521f5-8cb2-4a5c-a2a5-b5a11b2451ac" />

 
