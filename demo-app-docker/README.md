# Testing the demo-flask-app

## Building the demo-app container image
The following command will use the given Containerfile to build a container image with the specified dependencies. 

```bash
docker build . -f ./Containerfile -t demo-flask-app:0.1.0
```

The output of the above command will be a container image: `demo-flask-app:0.1.0`

## Running the demo-app container image
To run the demo-flask-app container image, use the following command:

```bash
docker run -p 5000:5000 --name demo-app-instance demo-flask-app:0.1.0
```

## Accessing the demo app
Open the following url `http://127.0.0.1:5000` in your browser. You should see a "Hello" message.

If you are successfully able to see the "Hello" message, it means your docker/container environment is functional.


## Cleaning up
After quiting the app, you can remove the container with the following command:

```bash
docker rm demo-app-instance
```