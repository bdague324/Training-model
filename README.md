# Training model
 Deploying - Training - saving model - having a web page

# Framework

We  need to create 3 AWS instances "Deep Learning Base AMI (Ubuntu 16.04) Version 21.0 - ami-045565871c0771faf" into one VPC
1. public instances - Ubuntu
1. public instances - Ubuntu
1. public instances - Ubuntu

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

This instance is used as the "front end". We need to install Apache & httpd.
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

## Third instance

This instance is used as the "back end". This last instance do the prediction.

In this instance, we need to install opencv to execute "keras_flask.py" file.