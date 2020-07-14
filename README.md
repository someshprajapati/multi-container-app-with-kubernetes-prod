# Multi Container App with Kubernetes for dev environment

### Apply the deployment `client-deployment` and service `client-cluster-ip-service`
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl apply -f k8s**
```
service/client-cluster-ip-service created
deployment.apps/client-deployment created
```

### Get the deployments details
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl get deployments**
```
NAME                READY   UP-TO-DATE   AVAILABLE   AGE
client-deployment   3/3     3            3           13s
```

### Get the pods
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl get pods**
```
NAME                                 READY   STATUS    RESTARTS   AGE
client-deployment-6fc4f8df6f-djm8d   1/1     Running   0          23s
client-deployment-6fc4f8df6f-mbbz2   1/1     Running   0          23s
client-deployment-6fc4f8df6f-vsrlw   1/1     Running   0          23s
```

### Get the services
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl get services**
```
NAME                        TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
client-cluster-ip-service   ClusterIP   10.97.99.237   <none>        3050/TCP   35m
kubernetes                  ClusterIP   10.96.0.1      <none>        443/TCP    28d
```

### Apply the deployment `server-deployment`, `worker-deployment` and service `server-cluster-ip-service`
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl apply -f k8s**
```
service/client-cluster-ip-service unchanged
deployment.apps/client-deployment unchanged
service/server-cluster-ip-service created
deployment.apps/server-deployment created
deployment.apps/worker-deployment created
```

### Get the pods
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl get pods**
```
NAME                                 READY   STATUS    RESTARTS   AGE
client-deployment-6fc4f8df6f-djm8d   1/1     Running   0          33m
client-deployment-6fc4f8df6f-mbbz2   1/1     Running   0          33m
client-deployment-6fc4f8df6f-vsrlw   1/1     Running   0          33m
server-deployment-5dd68746d-89vft    1/1     Running   0          5m57s
server-deployment-5dd68746d-tzb96    1/1     Running   0          5m57s
server-deployment-5dd68746d-vqrw2    1/1     Running   0          5m57s
worker-deployment-bd595c6b7-mlrg2    1/1     Running   0          19s
```

### Get the deployments details
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl get deployments**
```
NAME                READY   UP-TO-DATE   AVAILABLE   AGE
client-deployment   3/3     3            3           33m
server-deployment   3/3     3            3           6m9s
worker-deployment   1/1     1            1           31s
```

### Get the services
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl get services**
```
NAME                        TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
client-cluster-ip-service   ClusterIP   10.97.99.237    <none>        3000/TCP   68m
kubernetes                  ClusterIP   10.96.0.1       <none>        443/TCP    28d
server-cluster-ip-service   ClusterIP   10.97.239.165   <none>        5000/TCP   3m24s
```

### Get the logs of `server-deployment`
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl logs server-deployment-5dd68746d-89vft**
```
> @ start /app
> node index.js

Listening
```

### Get the logs of `worker-deployment`
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl logs worker-deployment-bd595c6b7-mlrg2**
```
> @ start /app
> node index.js
```

### Apply the deployment `redis-deployment` and service `redis-cluster-ip-service`
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl apply -f k8s**
```
service/client-cluster-ip-service unchanged
deployment.apps/client-deployment unchanged
service/redis-cluster-ip-service created
deployment.apps/redis-deployment created
service/server-cluster-ip-service unchanged
deployment.apps/server-deployment unchanged
deployment.apps/worker-deployment unchanged
```

### Get the services
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl get services**
```
NAME                        TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
client-cluster-ip-service   ClusterIP   10.97.99.237     <none>        3000/TCP   75m
kubernetes                  ClusterIP   10.96.0.1        <none>        443/TCP    28d
redis-cluster-ip-service    ClusterIP   10.106.171.185   <none>        6379/TCP   18s
server-cluster-ip-service   ClusterIP   10.97.239.165    <none>        5000/TCP   9m41s
```

### Apply the deployment `postgres-deployment` and service `postgres-cluster-ip-service`
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl apply -f k8s**
```
service/client-cluster-ip-service unchanged
deployment.apps/client-deployment unchanged
service/postgres-cluster-ip-service created
deployment.apps/postgres-deployment created
service/redis-cluster-ip-service unchanged
deployment.apps/redis-deployment unchanged
service/server-cluster-ip-service unchanged
deployment.apps/server-deployment unchanged
deployment.apps/worker-deployment unchanged
```

### Get the storageclass
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl get storageclass**
```
NAME                 PROVISIONER          AGE
hostpath (default)   docker.io/hostpath   28d
```

### Describe the storageclass
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl describe storageclass**
```
Name:            hostpath
IsDefaultClass:  Yes
Annotations:     kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"storage.k8s.io/v1","kind":"StorageClass","metadata":{"annotations":{"storageclass.kubernetes.io/is-default-class":"true"},"name":"hostpath"},"provisioner":"docker.io/hostpath","reclaimPolicy":"Delete","volumeBindingMode":"Immediate"}
,storageclass.kubernetes.io/is-default-class=true
Provisioner:           docker.io/hostpath
Parameters:            <none>
AllowVolumeExpansion:  <unset>
MountOptions:          <none>
ReclaimPolicy:         Delete
VolumeBindingMode:     Immediate
Events:                <none>
```

### Apply the PVC `database-persistent-volume-claim`
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl apply -f k8s**
```
service/client-cluster-ip-service unchanged
deployment.apps/client-deployment unchanged
persistentvolumeclaim/database-persistent-volume-claim created
service/postgres-cluster-ip-service unchanged
deployment.apps/postgres-deployment unchanged
service/redis-cluster-ip-service unchanged
deployment.apps/redis-deployment unchanged
service/server-cluster-ip-service unchanged
deployment.apps/server-deployment unchanged
deployment.apps/worker-deployment unchanged
```

### Get the persistent-volume details
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl get pv**
```
NAME                                       CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                                      STORAGECLASS   REASON   AGE
pvc-8860e4c2-90f3-4aee-9f8c-da85829a14cc   2Gi        RWO            Delete           Bound    default/database-persistent-volume-claim   hostpath                45s
```

### Get the persistent-volume-claim details
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl get pvc**
```
NAME                               STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
database-persistent-volume-claim   Bound    pvc-8860e4c2-90f3-4aee-9f8c-da85829a14cc   2Gi        RWO            hostpath       16m
```

### Get the pods
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl get pods**
```
NAME                                   READY   STATUS             RESTARTS   AGE
client-deployment-6fc4f8df6f-dx6jb     1/1     Running            0          2m9s
client-deployment-6fc4f8df6f-j8nzb     1/1     Running            0          2m9s
client-deployment-6fc4f8df6f-xp2x7     1/1     Running            0          2m9s
postgres-deployment-6767f87b54-p6b2m   0/1     CrashLoopBackOff   3          2m9s
redis-deployment-5f458546b8-wzggz      1/1     Running            0          2m9s
server-deployment-5dd68746d-7xz7l      1/1     Running            0          2m9s
server-deployment-5dd68746d-vdvww      1/1     Running            0          2m9s
server-deployment-5dd68746d-vztn2      1/1     Running            0          2m9s
worker-deployment-bd595c6b7-bpzxs      1/1     Running            0          2m9s
```

### Create the secret which we are going to use in postgres DB
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl create secret generic pgpassword --from-literal PGPASSWORD=test123**
```
secret/pgpassword created
```

### Get the secrets details
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl get secrets**
```
NAME                  TYPE                                  DATA   AGE
default-token-qfhgv   kubernetes.io/service-account-token   3      29d
pgpassword            Opaque                                1      16s
```

### Apply the changes after putting the secrets in `postgres-deployment` and `server-deployment`
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl apply -f k8s**
```
service/client-cluster-ip-service unchanged
deployment.apps/client-deployment unchanged
persistentvolumeclaim/database-persistent-volume-claim unchanged
service/postgres-cluster-ip-service unchanged
deployment.apps/postgres-deployment unchanged
service/redis-cluster-ip-service unchanged
deployment.apps/redis-deployment unchanged
service/server-cluster-ip-service unchanged
deployment.apps/server-deployment configured
deployment.apps/worker-deployment configured
```

### Get the pods for `ingress-nginx`
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl get pods -n ingress-nginx**
```
No resources found in ingress-nginx namespace.
```

### Use the `ingress-nginx` repo and apply the `ingress-nginx` controller
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.34.0/deploy/static/provider/cloud/deploy.yaml**
```
namespace/ingress-nginx created
serviceaccount/ingress-nginx created
configmap/ingress-nginx-controller created
clusterrole.rbac.authorization.k8s.io/ingress-nginx created
clusterrolebinding.rbac.authorization.k8s.io/ingress-nginx created
role.rbac.authorization.k8s.io/ingress-nginx created
rolebinding.rbac.authorization.k8s.io/ingress-nginx created
service/ingress-nginx-controller-admission created
service/ingress-nginx-controller created
deployment.apps/ingress-nginx-controller created
validatingwebhookconfiguration.admissionregistration.k8s.io/ingress-nginx-admission created
clusterrole.rbac.authorization.k8s.io/ingress-nginx-admission created
clusterrolebinding.rbac.authorization.k8s.io/ingress-nginx-admission created
job.batch/ingress-nginx-admission-create created
job.batch/ingress-nginx-admission-patch created
role.rbac.authorization.k8s.io/ingress-nginx-admission created
rolebinding.rbac.authorization.k8s.io/ingress-nginx-admission created
serviceaccount/ingress-nginx-admission created
```

### Get the pods for `ingress-nginx`
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl get pods -n ingress-nginx**
```
NAME                                        READY   STATUS      RESTARTS   AGE
ingress-nginx-admission-create-94zx5        0/1     Completed   0          106s
ingress-nginx-admission-patch-l9jzf         0/1     Completed   0          106s
ingress-nginx-controller-68679c6884-9w4s4   1/1     Running     0          116s
```

### Apply the service `ingress-service`
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl apply -f k8s**
```
service/client-cluster-ip-service unchanged
deployment.apps/client-deployment unchanged
persistentvolumeclaim/database-persistent-volume-claim unchanged
ingress.extensions/ingress-service created
service/postgres-cluster-ip-service unchanged
deployment.apps/postgres-deployment unchanged
service/redis-cluster-ip-service unchanged
deployment.apps/redis-deployment unchanged
service/server-cluster-ip-service unchanged
deployment.apps/server-deployment unchanged
deployment.apps/worker-deployment unchanged
```

### Get the kubernetes-dashboard used by Docker Desktop based Kubernetes
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **curl -O https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml**
```
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  4577  100  4577    0     0   9398      0 --:--:-- --:--:-- --:--:--  9398
```

### Apply the `kubernetes-dashboard` configuration
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl apply -f k8s/kubernetes-dashboard.yaml**
```
secret/kubernetes-dashboard-certs created
serviceaccount/kubernetes-dashboard created
role.rbac.authorization.k8s.io/kubernetes-dashboard-minimal created
rolebinding.rbac.authorization.k8s.io/kubernetes-dashboard-minimal created
deployment.apps/kubernetes-dashboard created
service/kubernetes-dashboard created
```

### Start the kubernetes proxy to check the dev app on `kubernetes-dashboard`
S😎MESH~[multi-container-app-with-kubernetes (master)]-$ **kubectl proxy**
```
Starting to serve on 127.0.0.1:8001
```



S😎MESH~[multi-container-app-with-kubernetes-production (master)]-$ ls -l
total 32
-rw-r--r--   1 someshprajapati  staff  13562 Jul 13 20:52 README.md
drwxr-xr-x@ 11 someshprajapati  staff    352 Jul 13 20:52 client
drwxr-xr-x  14 someshprajapati  staff    448 Jul 13 20:52 k8s
drwxr-xr-x@  9 someshprajapati  staff    288 Jul 13 20:52 server
drwxr-xr-x@  8 someshprajapati  staff    256 Jul 13 20:52 worker
S😎MESH~[multi-container-app-with-kubernetes-production (master)]-$
S😎MESH~[multi-container-app-with-kubernetes-production (master)]-$
S😎MESH~[multi-container-app-with-kubernetes-production (master)]-$ docker run -it -v $(pwd):/app ruby:2.4 sh
Unable to find image 'ruby:2.4' locally
2.4: Pulling from library/ruby
f15005b0235f: Pull complete
41ebfd3d2fd0: Pull complete
b998346ba308: Pull complete
f01ec562c947: Pull complete
2447a2c11907: Pull complete
1915e6344d7f: Pull complete
e867cf779be3: Pull complete
62af18474b7a: Pull complete
Digest: sha256:c15e108473724fd2fde6045657f905b411eea638be1ca97713a462e90db78da7
Status: Downloaded newer image for ruby:2.4
# gem install travis --no-rdoc --no-ri
ERROR:  While executing gem ... (OptionParser::InvalidOption)
    invalid option: --no-rdoc
#
# gem install travis --no-ri
ERROR:  While executing gem ... (OptionParser::InvalidOption)
    invalid option: --no-ri
# gem install travis
Fetching thread_safe-0.3.6.gem
Fetching multipart-post-2.1.1.gem
Fetching faraday-1.0.1.gem
Fetching faraday_middleware-1.0.0.gem
Fetching highline-2.0.3.gem
Fetching concurrent-ruby-1.1.6.gem
Fetching i18n-1.8.3.gem
Fetching tzinfo-1.2.7.gem
Fetching activesupport-5.2.4.3.gem
Fetching multi_json-1.15.0.gem
Fetching public_suffix-4.0.5.gem
Fetching addressable-2.7.0.gem
Fetching net-http-persistent-2.9.4.gem
Fetching net-http-pipeline-1.0.1.gem
Fetching gh-0.18.0.gem
Fetching json-2.3.1.gem
Fetching pusher-client-0.6.2.gem
Fetching launchy-2.4.3.gem
Fetching ffi-1.13.1.gem
Fetching ethon-0.12.0.gem
Fetching typhoeus-0.8.0.gem
Fetching travis-1.9.1.gem
Fetching websocket-1.2.8.gem
Successfully installed multipart-post-2.1.1
Successfully installed faraday-1.0.1
Successfully installed faraday_middleware-1.0.0
Successfully installed highline-2.0.3
Successfully installed concurrent-ruby-1.1.6

HEADS UP! i18n 1.1 changed fallbacks to exclude default locale.
But that may break your application.

If you are upgrading your Rails application from an older version of Rails:

Please check your Rails app for 'config.i18n.fallbacks = true'.
If you're using I18n (>= 1.1.0) and Rails (< 5.2.2), this should be
'config.i18n.fallbacks = [I18n.default_locale]'.
If not, fallbacks will be broken in your app by I18n 1.1.x.

If you are starting a NEW Rails application, you can ignore this notice.

For more info see:
https://github.com/svenfuchs/i18n/releases/tag/v1.1.0

Successfully installed i18n-1.8.3
Successfully installed thread_safe-0.3.6
Successfully installed tzinfo-1.2.7
Successfully installed activesupport-5.2.4.3
Successfully installed multi_json-1.15.0
Successfully installed public_suffix-4.0.5
Successfully installed addressable-2.7.0
Successfully installed net-http-persistent-2.9.4
Successfully installed net-http-pipeline-1.0.1
Successfully installed gh-0.18.0
Successfully installed launchy-2.4.3
Building native extensions. This could take a while...
Successfully installed ffi-1.13.1
Successfully installed ethon-0.12.0
Successfully installed typhoeus-0.8.0
Building native extensions. This could take a while...
Successfully installed json-2.3.1
Successfully installed websocket-1.2.8
Successfully installed pusher-client-0.6.2
Successfully installed travis-1.9.1
23 gems installed
# travis
Shell completion not installed. Would you like to install it now? |y| n
Usage: travis COMMAND ...

Available commands:

    non-API commands
        help           helps you out when in dire need of information
        version        outputs the client version
    API commands
        accounts       displays accounts and their subscription status
        console        interactive shell; requires `pry`
        endpoint       displays or changes the API endpoint
        lint           display warnings for a .travis.yml
        login          authenticates against the API and stores the token
        logout         deletes the stored API token
        monitor        live monitor for what's going on
        raw            makes an (authenticated) API call and prints out the result
        report         generates a report useful for filing issues
        repos          lists repositories the user has certain permissions on
        sync           triggers a new sync with GitHub
        token          outputs the secret API token
        whatsup        lists most recent builds
        whoami         outputs the current user
    Repo commands
        branches       displays the most recent build for each branch
        cache          lists or deletes repository caches
        cancel         cancels a job or build
        disable        disables a project
        enable         enables a project
        encrypt        encrypts values for the .travis.yml
        encrypt-file   encrypts a file and adds decryption steps to .travis.yml
        env            show or modify build environment variables
        history        displays a project's build history
        init           generates a .travis.yml and enables the project
        logs           streams test logs
        open           opens a build or job in the browser
        pubkey         prints out a repository's public key
        requests       lists recent requests
        restart        restarts a build or job
        settings       access repository settings
        setup          sets up an addon or deploy target
        show           displays a build or job
        sshkey         checks, updates or deletes an SSH key
        status         checks status of the latest build

run `/usr/local/bundle/bin/travis help COMMAND` for more info
# travis login
We need your GitHub login to identify you.
This information will not be sent to Travis CI, only to api.github.com.
The password will not be displayed.

Try running with --github-token or --auto if you don't want to enter your password anyway.

Username: someshprajapati
Password for someshprajapati: ************
Successfully logged in as someshprajapati!
# ls
app  bin  boot	dev  etc  home	lib  lib64  media  mnt	opt  proc  root  run  sbin  srv  sys  tmp  usr	var
# pwd
/
# cd /app
# ls
README.md  client  k8s	multi-kubernetes-production-28bdb0fdabb9.json  server  worker
#
# ls
README.md  client  k8s	server	service-account.json  worker
# travis encrypt-file service-account.json  someshprajapati / multi-container-app-with-kubernetes-production ^[[D^[[D^C
# travis encrypt-file service-account.json -r someshprajapati/multi-container-app-with-kubernetes-production
encrypting service-account.json for someshprajapati/multi-container-app-with-kubernetes-production
storing result as service-account.json.enc
storing secure env variables for decryption

Please add the following to your build script (before_install stage in your .travis.yml, for instance):

    openssl aes-256-cbc -K $encrypted_9f3b5599b056_key -iv $encrypted_9f3b5599b056_iv -in service-account.json.enc -out service-account.json -d

Pro Tip: You can add it automatically by running with --add.

Make sure to add service-account.json.enc to the git repository.
Make sure not to add service-account.json to the git repository.
Commit all changes to your .travis.yml.
# ls
README.md  client  k8s	server	service-account.json  service-account.json.enc	worker
#
# ls
README.md  client  k8s	server	service-account.json.enc  worker
# s
sh: 17: s: not found
# git status
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.DS_Store
	.travis.yml
	server/.DS_Store
	service-account.json.enc

nothing added to commit but untracked files present (use "git add" to track)
# rm .DS_Store server/.DS_Store
# git status
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.travis.yml
	service-account.json.enc

nothing added to commit but untracked files present (use "git add" to track)
# git add service-account.json.enc
# git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   service-account.json.enc

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.travis.yml

# git commit -m "Added encrypted google service account file"

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'root@ab78afb1e9da.(none)')
# exit
S😎MESH~[multi-container-app-with-kubernetes-production (master)]-$ s
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   service-account.json.enc

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.travis.yml

S😎MESH~[multi-container-app-with-kubernetes-production (master)]-$
S😎MESH~[multi-container-app-with-kubernetes-production (master)]-$ s
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   service-account.json.enc

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	.travis.yml

S😎MESH~[multi-container-app-with-kubernetes-production (master)]-$ git commit -m "Added encrypted google service account file"
[master a2fb305] Added encrypted google service account file
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 service-account.json.enc
S😎MESH~[multi-container-app-with-kubernetes-production (master)]-$ git push
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 12 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 2.63 KiB | 2.63 MiB/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote:
remote: GitHub found 1 vulnerability on someshprajapati/multi-container-app-with-kubernetes-production's default branch (1 high). To find out more, visit:
remote:      https://github.com/someshprajapati/multi-container-app-with-kubernetes-production/network/alert/client/package.json/axios/open
remote:
To github-personal:someshprajapati/multi-container-app-with-kubernetes-production.git
   6d8cd13..a2fb305  master -> master