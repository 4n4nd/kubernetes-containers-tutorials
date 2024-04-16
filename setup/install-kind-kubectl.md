# Setup Instructions for Kind and Kubectl

## Step 1: Install Docker
Before installing Kind, ensure Docker/Podman is installed and running on your machine.

### Windows and Mac:
- Download and install Docker Desktop from [Docker Desktop Windows](https://hub.docker.com/editions/community/docker-ce-desktop-windows)/[Docker Desktop Mac](https://docs.docker.com/desktop/install/mac-install/).

### Linux:
- Install Docker using your package manager, for example on Ubuntu:
  ```bash
  sudo apt update
  sudo apt install docker.io
  ```
- Start Docker and enable it to start on boot:
  ```bash
  sudo systemctl start docker
  sudo systemctl enable docker
  ```

## Step 2: Install Kind 
Kind can be installed directly from its GitHub releases page.

### For Linux and Mac (Similar instructions on Windows when using WSL):
Download using wget:
  ```bash
  wget https://kind.sigs.k8s.io/dl/v0.22.0/kind-$(uname)-amd64 -O ./kind # <- Download the kind binary>
  ```

  or
Download using curl:
  ```bash
  curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.22.0/kind-$(uname)-amd64 # <- Download the kind binary>
  ```
Make it executable:
  ```bash
  chmod +x ./kind # <- make it executable>
  sudo mv ./kind /usr/local/bin/kind # <- move it to the user's bin directory>
  ```

Now you should be able to run the kind command. To test it:
  ```bash
  kind --help
  ```
  You should see a help output:
  ```bash
  kind creates and manages local Kubernetes clusters using Docker container 'nodes'

  Usage:
    kind [command]

  Available Commands:
    build       Build one of [node-image]
    completion  Output shell completion code for the specified shell (bash, zsh or fish)
    create      Creates one of [cluster]
    delete      Deletes one of [cluster]
    export      Exports one of [kubeconfig, logs]
    get         Gets one of [clusters, nodes, kubeconfig]
    help        Help about any command
    load        Loads images into nodes
    version     Prints the kind CLI version

  Flags:
    -h, --help              help for kind
        --loglevel string   DEPRECATED: see -v instead
    -q, --quiet             silence all stderr output
    -v, --verbosity int32   info log verbosity, higher value produces more output
        --version           version for kind

  Use "kind [command] --help" for more information about a command.
  ```

Official instructions to install kind can be found [here](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)

## Step 3: Install kubectl

kubectl is the command-line tool used to interact with Kubernetes clusters. 
You can find the instructions to install kubectl at [the official kubernetes page](https://kubernetes.io/releases/download/#kubectl).


