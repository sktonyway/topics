# Date & Time
Computers follow unique approach to tackle date and time. Instead of keeping date and time into consideration, It follows the **Unix Epoch**, where we calculate date and time based on timestamps, as someone started a stopwatch on **01–01–1970 at 00.00.00 UTC**.
```js
 Date.now() // Gives number of milliseconds elapsed from 1st jan, 1970.
 ```

*So How do all computers show same time and are in sync?*

* The Hardware Clock, this keeps track of time even when offline.
* OS syncs periodically when connected atomic clocks on Internet, using NTP.
* Programming languages handle raw Unix timestamps and provide time as per context.

**For example:** A student in India, submit quiz at 5PM evening, server in US, keeps the current time-stamp instead of 5PM.

The Golden rule is *keep the Backend simple storing following Unix Epoch, and frontend do the rest*. This Idea is excellent:
* **Zero Ambiguity**, as the time is completely absolute.
* **Insane performance**, in calculation or sorting.
* **Perfect portability**, to various languages.

*What if users manipulate timestamps?*
* Using backend as ultimate source of truth.
* For high frequency financial trading or legal audits, We can use True Time & Vector Clocks. 
* We can also use Network Time APIs.

*What if my game is offline and I need accurate time?*
In this case, we can apply a simple approach, Instead of storing time, we store timestamps, zero when game started and so on, and sync when there is active Internet connection.