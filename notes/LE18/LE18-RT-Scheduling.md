# Introduction to Real-Time Scheduling

- **Real-Time Scheduling**: Refers to scheduling designed for real-time systems, where the primary goal is to respond to events within a specified time frame (real, wall-clock time).
- **Key Distinction**: The emphasis is on **predictability** rather than speed. Meeting deadlines is critical, and there are often consequences for missing them.

## Task Management and Terminology

- **Task**: Represents something that needs to be done. Tasks in real-time systems often correspond to threads performing specific work.
- **Task Types**:
  - **Hard Real-Time**: Deadlines must be met; failure to do so may lead to errors, system damage, or useless results (e.g., missile trajectory calculations).
  - **Soft Real-Time**: Deadlines are flexible; missing them degrades response quality but does not render the output completely useless.
  - **Firm Real-Time**: Deadlines are important, and responses arriving slightly late become useless but do not result in catastrophic system failure.

## Suitability of Standard Operating Systems for Real-Time

- **General Desktop OSes** (e.g., Linux, Windows, Mac OS) are not ideal for real-time systems, as they offer few or no guarantees about service time and response predictability.
  - **Examples**: Java's "stop-the-world" garbage collection can introduce unpredictable delays.

## Key Characteristics of Real-Time Systems

- **Determinism**: Predictable and guaranteed operations. While perfect determinism is unlikely, some level of guarantee is necessary.
- **Responsiveness**: Involves not only execution time but also the time to start handling interrupts, including potential interruptions by higher-priority tasks.
- **User (Administrator) Control**: Control levels may vary; typical OSes offer intermediate levels of control.
- **Reliability**: Ensures consistent, dependable operation.
- **Fail-Soft Operation**: Even if all tasks cannot be completed, the system should do its best to handle as many as possible.

## Scheduling Algorithm Requirements

- Real-time systems require different scheduling algorithms than general-purpose systems. Minimizing average response time and ensuring fairness are less relevant.
- **Immediate Preemption**: Non-preemptive algorithms are unsuitable; preemptive scheduling ensures critical tasks are prioritized.

## Real-Time Task Categories

1. **Fixed-Instance Tasks**: Tasks that occur a fixed number of times (usually just once).
2. **Periodic Tasks**: Tasks that repeat at regular intervals, characterized by:
   - **Period (\(\tau_k\))**: The interval between executions.
   - **Worst-Case Computation Time (\(c_k\))**.
   - **Utilization Calculation**:
     \[
     U = \sum_{k=1}^{n} \frac{c_k}{\tau_k}
     \]
   - If \(U > 1\), the system is overloaded and unable to guarantee task completion.

3. **Aperiodic Tasks**: Tasks that occur irregularly with no defined minimum interval between occurrences.
4. **Sporadic Tasks**: Similar to aperiodic tasks but with guaranteed minimum intervals between events and deadlines that must be met.

## Estimating Task Execution Times

- **Worst-Case Scenario** Assumption: Always consider the worst-case execution time to ensure deadlines are met.
- **Estimation Methods**:
  1. **Code Analysis**: Analyzing source code to predict the longest execution path, often leading to overestimation due to ignoring factors like pipelining and compiler optimizations.
  2. **Empirical Testing**: Using real-world measurements and simulations to approximate execution times.

## NASA/JPL Guidelines for Real-Time Code

1. No recursion or `goto` statements.
2. Loops must have fixed bounds.
3. No dynamic memory allocation after initialization.

## Handling System Overloads

- When the system is overloaded (e.g., too many periodic tasks), real-time scheduling techniques attempt to ensure critical tasks are prioritized and handled.

## Confidence Intervals in Estimation

- Estimation of worst-case runtime with confidence intervals, using statistical techniques to assert maximum runtime with a specified confidence level.

## Conclusion

Real-time scheduling is distinct from general scheduling due to its focus on predictability, deadlines, and system responsiveness. Tasks are categorized by timing constraints and execution regularity, with specific algorithms designed to meet stringent requirements. Accurate estimation of execution times is crucial, often relying on worst-case assumptions to guarantee predictable behavior.

This summary covers the key aspects and details of real-time scheduling presented in the lecture. If you have any specific areas you'd like to explore further, feel free to let me know!