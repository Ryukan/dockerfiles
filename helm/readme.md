### Build dockerfile

```bash
Without minikube
docker build -t helm:3.18.5 kubectl/.

With minikube
docker build --no-cache --build-arg MINIKUBE_PATH=$HOME -t helm:3.18.5 dockerfiles/helm/.
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
helm       3.18.5    032fc6d46498   About an hour ago   64.6MB
```



### Create an alias for ```helm``` via Docker
```bash
nano ~/.bashrc (if you use bash)
or
nano  ~/.zshrc (if you use Zsh)
```
```bash
# You can remove the minikube line if you don't use it.
alias helm='docker run -ti --rm --network host -v $(pwd):/apps -w /apps \
    -v ~/.kube:/root/.kube -v ~/.helm:/root/.helm \
    -v $HOME/.minikube:$HOME/.minikube \   
    -v ~/.config/helm:/root/.config/helm \
    -v ~/.cache/helm:/root/.cache/helm \
    helm:3.18.5'
```


```bash
source ~/.bashrc
or
source ~/.zshrc
```

