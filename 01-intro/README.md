Recommended development environment: Linux

Step 1: Download and install the Anaconda distribution of Python
wget https://repo.anaconda.com/archive/Anaconda3-2022.05-Linux-x86_64.sh
bash Anaconda3-2022.05-Linux-x86_64.sh
Step 2: Update existing packages
sudo apt update
Step 3: Install Docker
sudo apt install docker.io
To run docker without sudo:

sudo groupadd docker
sudo usermod -aG docker $USER
Step 4: Install Docker Compose
Install docker-compose in a separate directory

mkdir soft
cd soft
To get the latest release of Docker Compose, go to https://github.com/docker/compose and download the release for your OS.

wget https://github.com/docker/compose/releases/download/v2.5.0/docker-compose-linux-x86_64 -O docker-compose
Make it executable

chmod +x docker-compose
Add to the soft directory to PATH. Open the .bashrc file with nano:

nano ~/.bashrc
In .bashrc, add the following line:

export PATH="${HOME}/soft:${PATH}"
Save it and run the following to make sure the changes are applied:

source ~/.bashrc
Step 5: Run Docker
docker run hello-world
If you get docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create": dial unix /var/run/docker.sock: connect: permission denied. error, restart your VM instance.

Note: If you get It is required that your private key files are NOT accessible by others. This private key will be ignored. error, you should change permits on the downloaded file to protect your private key:

chmod 400 name-of-your-private-key-file.pem

#### Training a simple model for predicting the duration of a ride

- [ ]  **Downloading the data**
    - [ ]  We'll use [the same NYC taxi dataset](https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page), but instead of "**Green** Taxi Trip Records", we'll use "**Yellow** Taxi Trip Records".
    - [ ]  Download the data for January and February 2023.
    - [ ]  Read the data for January. How many columns are there?
- [ ]  **Computing duration**
    - [ ]  Now let's compute the `duration` variable. It should contain the duration of a ride in minutes.
    - [ ]  What's the standard deviation of the trips duration in January?
- [ ]  **Dropping outliers**
    - [ ]  Next, we need to check the distribution of the `duration` variable. There are some outliers. Let's remove them and keep only the records where the duration was between 1 and 60 minutes (inclusive).
    - [ ]  What fraction of the records left after you dropped the outliers?
- [ ]  **One-hot encoding**
    - [ ]  Let's apply one-hot encoding to the pickup and dropoff location IDs. We'll use only these two features for our model.
    - [ ]  Turn the dataframe into a list of dictionaries (remember to re-cast the ids to strings - otherwise it will label encode them)
    - [ ]  Fit a dictionary vectorizer
    - [ ]  Get a feature matrix from it
    - [ ]  What's the dimensionality of this matrix (number of columns)?
- [ ]  **Training a model**
    - [ ]  Now let's use the feature matrix from the previous step to train a model.
    - [ ]  Train a plain linear regression model with default parameters
    - [ ]  Calculate the RMSE of the model on the training data
    - [ ]  What's the RMSE on train?
- [ ]  **Evaluating the model**
    - [ ]  Now let's apply this model to the validation dataset (February 2023).
    - [ ]  What's the RMSE on validation?