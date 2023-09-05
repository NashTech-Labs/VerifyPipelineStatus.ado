# pipelineStatus

## Pipeline Requirements

The PipelineStatus pipeline requires the following parameters to be defined:
### Parameters:


| Name  | type | Default | Values | Opional/Required | Comments |
| :------------- | :-------------: | :------------- | :-------------: | :-------------: | :------------- |
| pipelineId | String | | | Required | This enables passing of Pipeline ID as a variable |
| resultFilter | String | succeeded | | Required | |
| buildNumber | String | | | Optional | |
| outputVariablePrefix | String |  | | Required | |
| pipelineDisplayName | String | | | Required | This enables to use different display name for the pipeline |
| executeCondition | Boolean | true | | Required | |
| buildIdstepName | String | | | Optional | This enables to use step name for the getLatestPipelineBuildId.yml template |
| maxIteration | String | | | Optional | |
| stagesToVerify | String | | | Optional | |
| buildSpec | String | | | Required | This enables to pass the buildID |
| failOnPipelineFailure | String | | | Optional | |
| verifyStepName | String | | | Required | This enables to use step name for the verifyPipelineStatus.yml template |
| stepDisplayName | String | | | Required | This enables to use different display name for the verifyPipelineStatus.yml template |

  These parameters provide multiple use case options for the PipelineStatus framework templates pipeline, executeCondition flag is used for the utilization of different templates as per the requirements.


## Use Cases


### 1. Publishing "pipelinestatus" as output (Output variable "BuilSummary" to be used in another dependent template)

You can use the "output variable" of this template as per the requirement. for example: 

```yaml

    # azure-pipeline.yaml
    resources:
    repositories:
    - repository: Template
        type: github
        name:  your_username/Repo_name
        ref: <respective branch name>
        endpoint: 'githubServiceConnectioNname'


    steps:
    - template: templates/verifyPipelineStatus.yml@Template
        parameters:
        BuildId: $buildId
        verifyStepName: VerifyClaimsPublishPipelines
        buildSpec: |
        [
            {
            "buildId": "${{ parameters.buildId }} "
            }              
        ]


```

The parameters are provided to configure the pipelineStatus pipeline according to the desired build configuration and stages.

Make sure to adjust the repository name, branch name, and parameter values according to your project's requirements.


