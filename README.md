# GitOps---ArgoCD
## GitOps Principles ##
GitOps is a framework where the entire code delivery process is controlled by via Git,which also includes infra and application definitions as code and automation to deploy changes and rollbacks.Gipops can be considered as a extension of Infrastructure as a code thst uses git as the version control system.
- Infra and application code must be declared in a decalrative state.
- All the declarative files also known as the desired state are stored in a git repository.
- GitOps operator,also known as software agent,automatically pull the desied state from Git and apply it in one or more environments or clusters.The GitOps operator can run in one of the clusters and can make or push changes to other clusters as well.
- The final principle is Reconciliation.the gitops operator also make sure that the entire sysytem is self-healing to reduce the risk of human-errors the operator continuously loops through 3 steps
    - Observe (checks the repo for any changes in the desired state)
    - Diff (compared the resources received from the previous step to the actual state of the cluster)
    - Act (it uses a reconciliation function and tries to match the actual state to the desired state)
