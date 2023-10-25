Hierarchical State Machine for Unity. Most likely I will rewrite it multiple times in the future but for now it suits my needs.
### There is no change in this fork yet

### TODO
- [ ] Rewrite everything

## How to Install
### Git Installation

If you have Git on your computer, you can open Package Manager indside Unity, select "Add package from Git url...", and paste link ```https://github.com/IntoTheDev/Hierarchical-State-Machine-for-Unity.git```

or

Open the manifest.json file of your Unity project.
Add ```"com.intothedev.ai": "https://github.com/IntoTheDev/Hierarchical-State-Machine-for-Unity.git"```

## Simple Example:
```csharp
public class TestStateMachine : HierarchicalStateMachine
{
	[SerializeField] private float _timeInPatrol = 1f;
	[SerializeField] private float _timeInIdle = 3f;

	protected override StateMachine Setup()
	{
		var patrolState = new PatrolState(transform, speed: 5f, randomizeStartSpeed: true);
		var emptyState = new Empty();

		var stateMachine = new StateMachine()
			.Configure(startState: patrolState)
			.AddTransition(patrolState, emptyState, new WaitFor(waitFor: 1f), reversed: false)
			.AddTransition(emptyState, patrolState, new WaitFor(waitFor: 3f), reversed: false);

		return stateMachine;
	}
}
```
