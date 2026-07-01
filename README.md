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
kubectl get pods -n argocd -w
<img width="1875" height="951" alt="image" src="https://github.com/user-attachments/assets/83d521f5-8cb2-4a5c-a2a5-b5a11b2451ac" />

- To access from the web browser ,either have to open the tunnel or do port forwarding
- for port forwarding use the command kubectl port-forward -n argocd svc/argocd-server 8080:443\
  (Port forwarding is a networking technique that allows external devices on the public internet to access a specific computer or service inside a private local network. It works by telling your router to send incoming traffic from a specific "port" directly to a designated device.)
<img width="824" height="101" alt="image" src="https://github.com/user-attachments/assets/bf6d31d8-c35b-4b8d-a57e-f0e5ec4f740c" />

- To open the tunnel use these steps
  - Edit the service and change the service type from cluster IP (by default) to Nodeport (kubectl edit svc argocd-server -n argocd -o yaml) so that we can access the service from the browser.
  - minikube service list -n argocd
  - minikube service argocd-service -n argocd (it will create a tunnel for http and https)
    - http://127.0.0.1:53220 (for http)
    - https://127.0.0.1:53221 (for https)
  
- Dex Server - Argo CD embeds and bundles Dex as part of its installation, for the purpose of delegating authentication to an external identity provider. Multiple types of identity providers are supported (OIDC, SAML, LDAP, GitHub, etc...). SSO configuration of Argo CD requires editing the argocd-cm ConfigMap with Dex connector settings.
- Application Controller is the core engineering engine of ArgoCD that continuously monitors running Kubernetes applications and reconciles their live state with the desired state specified in a Git repository. Operating as a Kubernetes StatefulSet, it drives the actual reconciliation and deployment loop that forms the foundation of the GitOps workflow
- Repo Server (argocd-repo-server) is an internal microservice responsible for maintaining a local cache of your Git/Helm repositories and generating the final Kubernetes manifests. It acts as a bridge between your source control and the deployment engine.
- API Server (deployed as the argocd-server pod) is the central gateway that sits between users, external tools, and the internal components of ArgoCD. It functions as a dual gRPC and REST server, exposing the endpoints consumed by the Web UI, CLI, and automated CI/CD pipelines.
- Notifications controller is a dedicated workload that monitors your Kubernetes cluster for Argo CD application events (such as sync success, failure, or degradation) and dispatches alerts to external platforms like Slack, email, and webhooks
  
<img width="1115" height="655" alt="image" src="https://github.com/user-attachments/assets/8f249227-b6ea-4ca9-9e2f-c60447c89dc0" />
<img width="1115" height="655" alt="image" src="https://github.com/user-attachments/assets/c4545c02-9358-422c-82dc-fbc0942c6d0a" />
<img width="944" height="532" alt="image" src="https://github.com/user-attachments/assets/e8557c06-e687-45b0-bc3a-95b0690cf676" />
<img width="1208" height="629" alt="image" src="https://github.com/user-attachments/assets/28138ecd-61a8-49ac-8ffa-ec2b24a694f6" />
<img width="1005" height="656" alt="image" src="https://github.com/user-attachments/assets/cae15930-8c01-41ad-a392-8f3e6161f94f" />
<img width="1172" height="604" alt="image" src="https://github.com/user-attachments/assets/8e044f13-741b-4598-a5e3-5f205df7c37a" />


