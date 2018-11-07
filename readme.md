# Continuous Integration for ROS on Windows

A common Azure DevOps pipeline template for ROS on Windows CI build. This template helps you to do CI build for your ROS repository against the ROS on Windows daily drops.

## Prerequisite
  * Make sure you have an Azure DevOps pipeline setup. If you don't, visit [here](https://docs.microsoft.com/en-us/azure/devops/pipelines/get-started/pipelines-sign-up) for getting started. It's free.
  * Learn how to create Azure DevOps pipeline from [here](https://www.youtube.com/watch?v=NuYDAs3kNV8)
  
## How to use this template
Firstly, go to your Azure DevOps project and create a new pipeline. As walking through the wizard, select `starter pipeline` and it will create a file of `azure-pipelines.yml` under the root of your ROS repository. And replace it with the following content:
```
resources:
  repositories:
    - repository: templates
      type: github
      name: seanyen-msft/rosonwindows_ci
      endpoint: seanyen-msft

jobs:
- template: build.yml@templates  # Template reference
  parameters:
    ros_metapackage: 'ros-melodic-desktop'
```

`resources` defines where to look for this common template. In this example, it defines a Github repository reference to `seanyen-msft\rosonwindows_ci` and use an `endpoint` to access it. Replace `endpoint` to your Github account (or your GitHub service connection name. By default, it is your Github account name).

`jobs\template` defines what template to be included. In this example, just include `build.yml@templates`, which means to refer to the `build.yml` under `seanyen-msft\rosonwindows_ci` GitHub repository.

under `template`, currently there is one required parameter `ros_metapackage` which is the basic image to check out for CI build. In this example, it will install `ros-melodic-desktop` before the CI build.

Once the wizard finishes, now you have your owned ROS on Windows CI build. 

You can also find an example from this [repo](https://github.com/seanyen-msft/common_msgs/tree/azure-pipelines)
