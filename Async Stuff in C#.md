
# 🔑 Keywords: async and await

async: Marks a method as asynchronous.
await: Pauses the method execution until the awaited task completes.

The async functions return Task or Task<T>

# What are Task or Task<T>
- these are objects (like promises) which contain several states.
-  Task<T> is a promise that will return a value of type T eventually.

  
-  Task: No return value (void equivalent for async)
-   Task<T>: Has a return value (int, string, User, etc.)

-   This task object can be inspected through its properties, awaited for result, handle errors from by using try-catch and cancelled.

## 🔹 Why not just use string instead of Task<string>?

Because async code is non-blocking. If we used just string, the method would have to wait and block the thread.

With Task<string>, it returns an object immediately which resolves later with the result when it is ready.

## States in Task

| Property                  | Meaning                                                                                         |
| ------------------------- | ----------------------------------------------------------------------------------------------- |
| `IsCompleted`             | `true` if the task finished (successfully, with error, or canceled)                             |
| `IsCompletedSuccessfully` | `true` if the task finished *without exceptions* and *not cancelled*                            |
| `IsFaulted`               | `true` if the task **threw an exception** (it failed)                                           |
| `IsCanceled`              | `true` if the task was **cancelled** via a `CancellationToken`                                  |
| `Exception`               | Holds the actual `Exception` if the task failed                                                 |
| `Status`                  | Enum with values like `WaitingToRun`, `Running`, `RanToCompletion`, `Faulted`, `Canceled`, etc. |

## Task vs Promise

| Concept          | C# Task / Task<T>      | JS Promise                |
| ---------------- | ---------------------- | ------------------------- |
| Awaiting         | await task             | await promise             |
| Success result   | task.Result (or await) | then()                    |
| Error handling   | catch (Exception)      | catch()                   |
| Cancellation     | CancellationToken      | Manual workaround         |
| State inspection | task.IsCompleted, etc. | ❌ (no direct state check) |

