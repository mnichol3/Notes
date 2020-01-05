# Managing Packagess in Anaconda

## Basic commands

* **List packages installed in the active environment**
  ```
  conda list
  ```
  
* **List packages installed in a deactived environment**
  ```
  conda list -n myenv
  ```
  
  
## Installing packages

* **Install packages into an existing environment**
  ```
  conda install --name [env] [package]
  ```
  
* **Install packages into the current environment**
  ```
  conda install [package]
  ```
  
* **Install a specific version of a package**
  ```
  conda install [package]=0.15.0
  ```
  
* **Install multiple packages at once**
  ```
  conda install [package1] [package2]
  ```
  
* **Install multiple packages at once & specify their versions**
  ```
  conda install [package1]=0.15.0 [package2]=7.26.0
  ```
  
## Updating packages

* **To update a package**
  ```
  conda update [package]
  ```
  
* **To update Python**
  ```
  conda update python
  ```
  
* **To update conda itself**
  ```
  conda update conda
  ```
  
## Removing packages

* **Remove a package from an environment**
  ```
  conda remove -n [env] [package]
  ```
  
* **Remove a package from the current environment**
  ```
  conda remove [package]
  ```
  
* **Remove multiple packages at once**
  ```
  conda remove [package1] [package2]
  ```
