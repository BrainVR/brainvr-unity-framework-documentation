So you want to implement your first experiment? First go to the [getting started](getting-started.md) section and try that the framework runs and logs. If you don¨t encounter any issues, it is time to implement your first custom script.

There are several staps you will need to do to create a new experiment in this framework.

1. Create experiement class
2. Create experiemnt settings class and creatting settings asset
3. Setting up the scene according to your liking
4. Modify the experiment class

## Creating experiment class

### Required functions
Below is a complete list of functions that need to be implemented in the Expeirment flow. Many of these functions can effectively remain empty without hindering your expeirment performance. They are just there in case you need them.

Experiment functions:
```{c#}
public abstract void AddSettings(ExperimentSettings settings);
void OnExperimentInitialise();
void AfterExperimentInitialise();
void OnExperimentSetup();
void AfterExperimentSetup();
void OnExperimentStart();
void AfterExperimentStart();
void OnExperimentFinished();
void AfterExperimentFinished();
void OnExperimentClosed();
void AfterExperimentClosed();
```

Trial functions:
```{c#}
void OnTrialSetup();
void AfterTrialSetup();
void OnTrialStart();
void AfterTrialStart();
void OnTrialFinished();
void OnTrialForceFinished(){FinishTrial();};
void AfterTrialFinished();
void OnTrialClosed();
void AfterTrialClosed();
bool CheckForEnd();
```

Logging Functions:
```{c#}
public abstract string ExperimentHeaderLog();
```

## Creating experiment settings class


Need
- Settings object
- Experiemnt manager
- PlayerController - some sort of

Place setting asset on the settings game object. When scene loads, this will get registered in the experiment manager


