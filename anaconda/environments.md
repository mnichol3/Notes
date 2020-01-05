# Managing Environments in Anaconda

## Basic commands

* **Activate an environment**
  ```
  conda activate myenv
  ```
  
    where `myenv` is the name of the environment
  
* **Deactivate an environment**
  ```
  conda deactivate
  ```

* **View a list of your environments**
  ```
  conda env list
  ```
  
  or 
  
  ```
  conda info --envs
  ```
  
* **View a list of packages in your environment**
  * If the environment is not activated:
    ```
    conda list -n myenv
    ```
    
  * If the environment is active:
    ```
    conda list
    ```
    
  * To see if a specific package is installed in your environment
    ```
    conda list -n myenv scipy
    ```
  
## Creating an environment

### Creating an environment by command

* **Create a basic environment**
  ```
  conda create --name newenv
  ```
  
* **Create an environment with a specific version of Python**
  ```
  conda create --name newenv python=3.6
  ```
  
* **Create an environment with a specific package**
  ```
  conda create --name newenv scipy
  ```
  
  or, to install a specific package version.
  ```
  conda create --name newenv scipy=0.15.0
  ```
  
* **Create an environment with a specific version of Python and multiple packages**
  ```
  conda create --name newenv python=3.6 scipy=0.15.0 pandas scikit-learn
  ```
  
### Creating an environment from a `.yml` file
```
conda env create -f environment.yml
```


### Cloning an environment
```
conda create --name myclone --clone myenv
```


