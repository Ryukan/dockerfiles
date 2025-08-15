### Build dockerfile

```bash
Without minikube
docker build -t kubectl:1.30.1 kubectl/.

With minikube
docker build --no-cache --build-arg MINIKUBE_PATH=$HOME -t kubectl:1.30.1 dockerfiles/kubectl/.
```
* ```-t my-image-name:tag```: This assigns a name and an optional tag to your image. You can use latest or any version/tag of your choice.
* ```.```: Indicates that Docker should look for the Dockerfile in the current directory.

### Verify the Build
```bash
docker images
```
You should see something like this:
```bash
REPOSITORY    TAG       IMAGE ID       CREATED             SIZE
kubectl       1.30.1    032fc6d46498   About an hour ago   64.6MB
```

### Test the image
```bash
docker run --rm -it -v $HOME/.kube:/root/.kube kubectl:1.30.1 version
```
* ```--rm```: Removes the container after the command has been executed.
* ```-it```: Start the container in interactive mode.
* ```-v $HOME/.kube:/root/.kube```: Mount your kubeconfig configuration file (so that kubectl can access your Kubernetes cluster).

You should see something like this:
```bash
Client Version: v1.30.1
Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3
```

### Create an alias for ```kubectl``` via Docker
```bash
nano ~/.bashrc (if you use bash)
or
nano  ~/.zshrc (if you use Zsh)
```
Without Minikube
```bash
alias kubectl='docker run --rm -it -v $HOME/.kube:/root/.kube kubectl:1.30.1'
```
With Minikube
```bash
alias kubectl='docker run --rm --network host -it -v $HOME/.kube:/root/.kube -v $HOME/.minikube:$HOME/.minikube kubectl:1.30.1'
```

```bash
source ~/.bashrc
or
source ~/.zshrc
```

### Test the alias (Launch the command)
```bash
kubectl version
```

You should see something like this:
```bash
Client Version: v1.30.1
Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3
```