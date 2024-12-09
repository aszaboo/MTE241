# Real-Time Scheduling Algorithms

## Earliest Deadline First (EDF)

- **Concept**: Tasks are scheduled based on their deadlines. The task with the earliest deadline is chosen first.
- **Example**:
  - Consider an assignment due today, another due next Tuesday, and an exam next month. The algorithm prioritizes tasks by their deadlines, completing the assignment due today first.
  - When a task completes, the next task with the soonest deadline is chosen. If a new task arrives with a sooner deadline while a current task is executing, the current task is suspended, and the new task is scheduled.
- **Key Property**: If there exists a feasible way to schedule all tasks such that all deadlines are met, EDF will find it.

## Deadline Interchange Problem

- **Issue**: This approach can lead to a scenario resembling **priority inversion**.
  - **Example**: Task A holds a resource needed by task B, which has a sooner deadline. If there are tasks C, D, E, etc., also requiring this resource, task A could be delayed indefinitely, even if task B misses its deadline.
- **Solution**: Assign task A a new deadline, equal to the soonest deadline of the tasks waiting for the resource (similar to priority inheritance).

## Least Slack First (LSF)

- **Slack**: The time remaining before a task must start to meet its deadline.
  - **Example**: If a task needs 10 ms to execute and its deadline is 50 ms away, it has 40 ms of slack time.
- **Concept**: Tasks with the least slack are given the highest priority. This helps prioritize tasks most at risk of missing their deadlines.

## Rate-Monotonic Scheduling (RMS)

- **Concept**: Tasks with shorter periods (i.e., tasks that execute more frequently) are assigned higher priority.
- **Limitations**: This algorithm is not optimal and may fail to meet all deadlines even if utilization is less than 1.
  - **Example**: For tasks (1, 4), (3, 7), and (3, 10), where utilization is 137/140, EDF would succeed, but RMS may fail.

## Deadline Monotonic Scheduling

- A variant of RMS where priorities are assigned based on deadlines. Tasks with the shortest deadlines receive the highest priority.

## Aperiodic Servers

- **Challenge**: Scheduling tasks with soft deadlines can be difficult since distinguishing between soft and hard real-time tasks isn't always straightforward.
- **Approach**: Aperiodic or soft-deadline tasks are generally assigned lower priority compared to firm or hard real-time tasks.

### Polling Server

- **Concept**: Acts as a periodic hard-deadline task with a fixed execution budget and period. During this period, aperiodic tasks are executed sequentially.
- **Behavior**:
  - If there are too many tasks, they are carried over to the next execution period.
  - If there are too few tasks, any remaining budget is discarded.

### Deferrable Server

- **Improvement over Polling Server**: Instead of discarding unused time, the server saves it for later use within the same period.

### Sporadic Server

- **Concept**: Allows unused periods to be saved indefinitely, with a replenishment mechanism to spread execution more evenly over time.

## Multiprocessor Scheduling

- **Key Questions**:
  1. Is preemption permitted?
  2. Is job migration permitted?
  3. Is job parallelism permitted?

### Approaches to Multiprocessor Scheduling

1. **Global Scheduling**: All tasks are placed in one queue, and any processor can execute any task.
2. **Partitioned Scheduling**: Tasks are statically assigned to specific processors.
   - **Limitation**: May lead to low utilization (only 50% utilization in some cases).

### Semi-Partitioned Scheduling

- Combines elements of global and partitioned approaches. Some tasks are fixed to specific processors, while others may migrate.

## P-Fairness (Proportional Fairness)

- **Goal**: Allocate CPU time so tasks make progress at steady rates.
- **Concept**: An application requests \(x_i\) time units every \(y_i\) time quanta. The system guarantees between \(\lfloor x_i/y_i \times T \rfloor\) and \(\lceil x_i/y_i \times T \rceil\) quanta of service over any period \(T\).
- **Lag**: Measures the difference between allocated and expected CPU time. Tasks with positive lag require more CPU time, while tasks with negative lag have had more than their fair share.
- **P-Fair Algorithm**:
  1. Schedule all urgent tasks (lag > 0).
  2. Do not schedule tasks with negative lag.
  3. Schedule remaining tasks in order of highest lag until capacity is filled.
- **Goal**: Keep the lag between -1 and +1 for all tasks.
