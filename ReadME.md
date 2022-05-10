# Objective
<br>
The aim of this git page is to correctly guide users through a tutorial of converting https://www.kaggle.com/c/nlp-getting-started competition notebook into a kubeflow pipeline.<br><br> 
There are 3 different ipynb files in this repo. The one ending with -orig is the original one from the competition, the one ending with -kpf uses vanilla kubeflow to create the pipeline and the one ending with -kale uses kale to build the kubeflow pipeline. <br>
<br>
Now we have two diiferent ways of running both the vanilla and the Kale version. The instructions to run the notebooks are as follows:
<br>
# Running the vanilla notebook - KFP Pipeline Setup

The initial few steps to run either notebooks are exactly the same. Then after the fourth step there is a big difference on how to convert the original competition notebook into a kubeflow pipeline, this can be clearly seen below. <br>

Step 1 : Go to Kubeflow Dashboard and on the left panel click on Notebooks.
<br>
Step 2 : Click on the “+ New Notebook” button on the top right and create a notebook by giving it a name. Change the Workspace volume from from 5 GB to 50 GB, and change the requested memory to 6 GB.

Step 3 : After the set up is done, click on the Connect button next to the notebook you just created. It will take you to a JupyterLab.


Step 4 : In the JupyterLab launcher start a new terminal session to clone the github repo. In the terminal enter the following commands:

$ git clone https://github.com/AnkitRai-22/natural-language-processing-with-disaster-tweets-kaggle-competition

Step 5 : After succesfully cloning the repo, double click on the "natural-language-processing-with-disaster-tweets-kaggle-competition" to go to the github repo. Then open the notebook named "natural-language-processing-with-disaster-tweets-kfp.ipynb" by double-clicking on this name in the left hand directory structure, and to run it click on the "restart the whole kernel and re-reun the whole notebook"(fast-forward logo-ed) button in the top menu of the notebook.
<br>
The differences in defining the KFP notebook from the original one require us to make note of the following changes: <br> <br>

 - Defining Functions - The function should be defined in such a way that every library which is being used inside it should be imported inside it. 

 - Passing data between components -  To pass big data files the best way is to use KPF components such as InputPath() and OutputPath() which store the location of the input and output files(generally we use this for big files such as CSV or big TEXT files). To download the data the best way is to pass an url and download it, use it in the function and store the output as a pickle file in the OutputPath() location and pass the OutputPath() as InputPath() to the next component and then extract the contents of the pickle file.

 - Converting the Functions into Components - We use: 

kfp.components.create_component_from_func()

This function takes mainly three arguments. The first one is the name of the function which is to be converted into a component, the second one is the list of packages to be installed as a list under the argument name as packages_to_install=[], and the final argument is the output_component_file which is defined by us as a .yaml file.


 - Defining Pipeline function -  We now define pipeline using @dsl.pipeline to define the pipeline. We add a name and description to the pipeline, and then define a function for this pipeline, which has arguments passed on, which are used as input to the components created earlier. We then pass the output of one component as input argument to the next component. 


 - Running the pipeline - To run the pipeline we use kfp.Client(), and create an object of the class and then use create_run_from_pipeline_func function to run the pipeline by passing it the name of the pipeline and the arguments which are required as input.


<br><br>
# Running the Kale Version

The steps to deploy the pipeline using Kale are as follows:<br><br>

Step 1 : Go to Kubeflow Dashboard and on the left panel click on Notebooks.


Step 2 : Click on the “+ New Notebook” button on the top right and create a notebook by giving it a name. Change the storage for the volume from from 5 GB to 50 GB.




Step 3 : After the set up is done, click on the Connect button next to the notebook you just created. It will take you to a JupyterLab.


Step 4 : In the JupyterLab launcher start a new terminal session to clone the github repo. In the terminal enter the following commands:

$ git clone https://github.com/AnkitRai-22/natural-language-processing-with-disaster-tweets-kaggle-competition


Step 4 : Open the python notebook named: nlp_getting_started.ipynb in the JupyterLab launcher.

Step 7 : After opening of the notebook run the first cell with the following code:

pip install -r requirements.txt

Step 8 : Restart the kernel

Step 9 : Enable Kale by clicking on the Kale menu option in the left-side panel and give a name and a description to the pipeline. The video link for creating the pipeline is here. This should help in using Kale UI.


Step 10 : Click the “Run and Compile” button at the bottom of the Kale menu then click to view the pipeline in real-time.


## Check out the blog to learn more! Link to be added soon!
