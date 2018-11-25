As you read in [previous chapter](expeirment-flow.md), each new expeirment inherits from the `BrainVR.UnityFramework.Experiments.BaseExperiment` class. This class has a certain logic and flow that is described below.

## Experiment flow
Each experiment is separated to following phases:

1. `ExperimentInitialise`
2. `ExperimentSetup`
3. `ExperimentStart`
4. `ExperimentFinish`
5. `ExperimentClose`

Trials run only after Experiment is started and before it is finished. Initialisation and setup are used for instantiating objects and setups that need to be done in certain order. We provide two separate functions just in case somebody needs it. 

Unlike Trial functions, experiment functions cannot be run separately, they are run in blocks of 1-3 and 4-5 with `StartExperiment` and `FinishExpeirment` functions. You don't necessarily need to use `FinishExpeirment` function, as the experiment finishes automatically if the  `CheckForEnd()` function evaluates to true.

Each stage has `OnExperiment[Setup/Start ..]` and `AfterExperiment[Setup/Start..] abstract functions that need to be implemented. These functions can remain empty, but Experiment will call them during execution.

Example:
```{c#}
private void ExperimentSetup()
{
    OnExperimentSetup();
    if (ShouldLog) StartLogging();
    SendExperimentStateChanged(ExperimentState.WaitingToStart);
    ExperimentState = ExperimentState.WaitingToStart;
    AfterExperimentSetup();
}
```

You can see that the `Experiment` setup function will eventually call both `OnExperimentSetup` and `AfterExperimentSetup` functions so your child needs to implement them. usually `On` function is called in the very beginning, and `After` function at an end, but there are some exceptions that should make things cascade less violently. E.g. `ExperimentStart` actually calls `AfterExpeirmentStart` function before it calls `TrialSetup`. It is a little bit confusing. This is because otherwise trial would be already already setup, when the callback would return to the function and started calling After function. 

If these exceptions or other positioning causes problems with timing, feel free to change the order in the Experiment class or sent me an email.

## Trial flow

Each Trial is set to following stages:

1. `Setup`
2. `Start`
3. `Finish`
4. `Close`

Each stage has `OnTrial[Setup/Start ..]` and `AfterTrial[Setup/Start ..]` functions that need to be implemented in a similar way as the expeirment does.

## IMPORTANT: How to start a trial
Because of **security** checks in the experiment flow, the framework will NOT allow you to "start" a trial before it has been properly initialised/setup. And because the setup only changes the trial state AFTER all the setup functions did their job, your only option to *start* a trial after it is setup is to put `StartTrial()` funciton in the `AfterTrialSetup()` override. If you put it in the `OnTrialSetup()`, then it won't actually start because of the checks that happen.

### Force finishing trial
I provide special case for skipping or force finishing trials. Because sometimes quitting trial in a middle can have unexpected effects (for example you subscribed to an event and never unsubscribed, because that happens before trial is finished). Function `TrialSetNext(int trialNumber)` force finishes a trial. Default virtual behaviour is to `FinishTrial()`, but you can override this. Don't forget to `FinishTrial()` in the override (or call base);

