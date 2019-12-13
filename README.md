# Training model
 Deploying - Training - saving model - having a web page

# Framework

The architecture is splited into 3 instances
* to avoid for example interuption in the production (update,...)
* to have more flexibility

So we need to create 3 AWS instances "Deep Learning Base AMI (Ubuntu 16.04) Version 21.0 - ami-045565871c0771faf" into our VPC:
1. public instances - Ubuntu (instance for training the model)
1. public instances - Ubuntu (Front end)
1. public instances - Ubuntu (Back end).

The **front end** interacts with the user, gathers all it needs and send it to the back end.
The **back end** computes and send back information to the front end to be displayed to the end user.

# Database used

We are going to use the MNIST database developped by Yann LeCun. It is a dataset composed of 60000 examples of written numbers (from 0 to 9). We will have 60 examples as our test set.

## First instance

This instance is used to train the model. We will need to:
* install Jupyter
* train our model (provided)
* save our model
* create a virtual environment

We will use Keras and Tensorflow. Once the model is trained and saved we shut our instance down.

Herebelow the code used:

```
wget https://repo.anaconda.com/archive/Anaconda3-2019.03-Linux-x86_64.sh
sudo bash Anaconda3-2019.03-Linux-x86_64.sh #Answer yes to all questions
export PATH=~/anaconda3/bin:$PATH #If conda command is not found after installation

jupyter notebook --ip=0.0.0.0 --no-browser

conda create -n nameofyourenv python=3.6
conda install nb_conda "This needs to be done outside your virtual env

conda activate nameofyourenv
conda install ipykerne
ipython kernel install --user --name=nameyouwanttodisplay

#Here you are in your virtual environment
#What you need to install
#AT LEAST
#Keras (don't mind the version)
#Tensorflow 1.8
pip install --upgrade tensorflow

```

## Second instance

This instance is a webserver (web app) used as the "front end". We will need to:
* install the webserver,
* deploy the files in the right place,
* install Apache server & httpd.
* test if it works.

```
sudo apt-get update
sudo apt-get install yum
sudo yum update -y
sudo service httpd start
sudo yum -y install httpd
sudo apt install apache2
sudo ufw app list

sudo systemtl status apache2

sudo apt-get install git
git clone https://github.com/leodsti/AWS_Tutorials.git

~/AWS_Tutorials/MNIST$ sudo mv index.html /var/www/html/

```
### Security Group & port choice

### IP changes
```
Sudo vi index.html

# Type “I” to insert text- Put the IP number of the backend Instance (in the url field)
# then controle C

:wq

# :wq is to write and quit
```
Here below a figure representing the opened file using the VI_editor

![Légende](IP_change.png)

## Third instance (Flask (equivalent of NodeJS))

This instance is used as the "back end". This last instance do the prediction. It is our application. Our model is saved in our Back end. Our instance is installed into the public subnet but without a public IP.

In this instance, we need to install opencv to execute "keras_flask.py" file.
