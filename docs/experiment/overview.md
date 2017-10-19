Experiment class is the major part of this framework. It is a Unity component, that can be attached to an empty object, but it is usualy taken care of with [ExperimentManager](../objects/experiment-manager.md). It has a certain enforced [flow](flow.md) that you can extend. This class is responsible for logging experiment state changes and events, keeping clear structure of function calls, keeps state of trials nad expeirment itself etc.

## Experiment

### Variables
Variable      | Purpose       
------------- | ------------- 
[Name](class.md#aame) | Name of the experiment. important for serialisation
[TrialNumber](class.md#tiralnumber) | Tracks the trial number.
[ExperimentNumber](class.md#experimentnumber) | In case we are runnign multiple experiments at the same time.
[ExperimentState](class.md#experimentstate) | Tracks the state of the expeirment

### Events
Event         | Purpose       
------------- | ------------- 
[ExpeirmentEventSent](class.md#expeirmenteventsent)| Sends info about event being sent. Mostly for logging purposes.
[TrialStateChanged](class.md#trialstatechanged) | Sends info about change in trial state
[TrialEventSent](class.md#trialeventsent) | Sends info for logging purposes.
[MessageSent](class.md#messagesent) | Generic message event to logger.

### Functions
Function         | Purpose       
---------------- | ------------- 
[StartExperiment](class.md#startexpeirment) | Starts the expeirment if possible.
[TrialSetNext](class.md#trialsetnext) | Sets the trial to the next one if possible.
[ForceNextTrial](class.md#forcenexttrial) | Forces next trial.
[ForceSetTrial](class.md#forcesettrial) | Forces the trial to be set to designated number
[ForceFinishTrial](class.md#fircefinishtrial) | Finishes the trial in any state
[FinishExperiment](class.md#finishexpeirment)| Finishes the expeirment immediately
[AddSettings](class.md#addsettings) | Override to allow adding different settings to implemetned expeiremnts
[ExperimentHeaderLog](class.md#expeirmentheaderlog) | Logs the speicific header for each expeirment


## Experiment Settings

Class `ExpeirmentSettings` allow custom parameters for each expeirment. It allows serialisation and deserialisation and takes variable parameters according to your design.



## Experiment Results

Class `ExperimentResults` is designed to take 

### Attributes
the class has two custom attributes `[TestData]` and `[ResultData]` to allow sequential and separate parsing. Just tag everything you want in your results as `[ResultData]` nad all the raw data as `[TestData]`. Unmarked values are not parsed in the `Save()` function.
