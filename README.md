<div align="center"> <h1> MLops-Project </h1> </div>

<div align="center"> <h3> problem Statement </h3> </div>

> 1. Create container image that’s has Python3 and Keras or numpy  installed  using dockerfile 
> 2. When we launch this image, it should automatically starts train the model in the container.
> 3. Create a job chain of **job1, job2, job3, job4** and **job5** using build pipeline plugin in Jenkins 
> 4.  **Job1** : Pull  the Github repo automatically when some developers push repo to Github.
> 5.  **Job2** : By looking at the code or program file, Jenkins should automatically start the respective machine learning        software installed interpreter install image container to deploy code  and start training( eg. If code uses CNN, then Jenkins      should start the container that has already installed all the softwares required for the cnn processing).
> 6. **Job3** : Train your model and predict accuracy or metrics.
> 7. **Job4**: if metrics accuracy is less than 90%  , then tweak the machine learning model architecture.
> 8. **Job5**: Retrain the model or notify that the best model is being created
> 9. Create One extra job job6 for monitor : If container where app is running. fails due to any reason then this job should 
> automatically start the container again from where the last trained model left

**Note** - Here we are using the Fashion Dataset.For Training the Model.

**Job-1**
* In The job first we are pulling the data from Mlops-Project Directory . for this we are use the git plugin.
* Downloaded data we are cp into one folder.

![job1](https://github.com/Sumit-Rasal/MLops-Project/blob/master/screenshot/Screenshot%20from%202020-05-25%2018-55-34.png)

![job-1](https://github.com/Sumit-Rasal/MLops-Project/blob/master/screenshot/Screenshot%20from%202020-05-25%2018-55-38.png)

**Job-2**
* In the Job-2 we have to Find out which type of code it is.( code may be of - CNN, simple python code). For this we are using the grep command and retriving the **Conv2D** word because Conv2D is the unique word alwayes use in the CNN.
* After detecting the code,launching the respective container. They have all software. For launching the code we are using the Docker run command.

![job2](https://github.com/Sumit-Rasal/MLops-Project/blob/master/screenshot/Screenshot%20from%202020-05-26%2014-39-06.png)

**Job-3**
* We are Training the model and storing the accuracy value in a one file. For Training purpose we are use the exec concept of docker.

![job2](https://github.com/Sumit-Rasal/MLops-Project/blob/master/screenshot/Screenshot%20from%202020-05-26%2014-40-00.png)

* The code we are using for Storing accuracy Data in the file are given below.

![job2](https://github.com/Sumit-Rasal/MLops-Project/blob/master/screenshot/Screenshot%20from%202020-05-26%2016-57-36.png)


**Job-4**
* Here we are checking the accuracy.If the accuracy less than 90% then we are tweak the machine learning model architecture.
* In the tweak we are  _adding the convolution layer_ , also increase the _epoch_

![job2](https://github.com/Sumit-Rasal/MLops-Project/blob/master/screenshot/Screenshot%20from%202020-05-26%2014-44-51.png)

**Job-5**
* We are reading the file where we are store the accuracy In my case I store in the sumit.txt file.
* After Reading the File. We are send the Notification. For sending The Notification we are using the Email Notification  plugin In the Jenkins

How to Configure for Email Notification
![job-5](https://github.com/Sumit-Rasal/MLops-Project/blob/master/screenshot/Screenshot%20from%202020-05-28%2009-32-28.png)

![job-5](https://github.com/Sumit-Rasal/MLops-Project/blob/master/screenshot/Screenshot%20from%202020-05-28%2009-39-16.png).

**Job-6**
* Here we are monitoring the container. For monitoring we are using while loop.
* while Loop monitoring the container each and very second.

![job-5](https://github.com/Sumit-Rasal/MLops-Project/blob/master/screenshot/Screenshot%20from%202020-05-28%2009-31-35.png)

``` 
while true;
do
if [ `sudo docker ps | sudo grep -ow mlops` == "mlops" ]
then
echo ''
else
sudo docker run -itd -v /root/Desktop/mlops-project/:/root/mlops/ --name mlops sumit301/ml:v1
fi
done
```
* Output of The Job.

![job-5](https://github.com/Sumit-Rasal/MLops-Project/blob/master/screenshot/Screenshot%20from%202020-05-28%2009-20-21.png)

#### Grapical View of Jenkins Delivery pipline.















