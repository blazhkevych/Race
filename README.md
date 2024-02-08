# Topic
In this lab, we will reinforce our knowledge of working with Java streams and also look at additional Java Core classes.

## Initial Data
Java core libraries.

## Tasks
### Create a Race App

1. **Create a Car class**

   a. Create a `Car` class

   b. Add 2 main fields: `name`, `maxSpeed`

   c. Create a `Runnable` constructor


2. **Create a RaceCarRunnable class**

   a. Create a `RaceCarRunnable` class that extends `Car`

   b. Add fields `passed` (distance traveled), `distance` (length of the route), `isFinish` (race completion flag)

   c. Implement a constructor with parameters of the `Car` class and a `distance` field

   d. Implement the `getRandomSpeed` method, in which the speed of the car will be determined by the interval (min: `maxSpeed/2`, max: `maxSpeed`)

   e. Display a message using the template ("carName => speed: 123; progress: 55/350", where `carName` is the name of the car, `123` is the current speed, `55` is the distance traveled, `350` is the length of the route)


3. **Simulation of Car Movement**

   a. In the `run` method, define a loop `while(!isFinish)`

   b. In the loop, every second (`sleep(1000)`), calculate the distance traveled (in meters), knowing the current speed (from the `getRandomSpeed` method) and the time interval of 1s.

   c. Add verification. If the car has covered a distance >= the length of the track, set the `isFinish` flag to true.


4. **Create a Race Class**

   a. Create a `Race` class with the main method

   b. Create an `ArrayList<RaceCarRunnable>` called `cars` and add several “race cars” to it

   c. Create an `ArrayList<Thread>` and initialize it with machine thread objects. (`new Thread(car)`)


5. **Centralized Start of the Race**

   a. Create a static method `static void startRace(List<Thread> cars)` in the `Race` class

   b. In the method, create a thread based on an anonymous class (`new Thread(new Runnable() {...})`)

   c. In the `run` method, define a countdown cycle to start.

   d. Display messages at 500ms intervals: "3...", "2...", "1...", "GO!!!"

   e. Immediately after "GO!!!", create a loop through the list of threads and execute `start()` on each race car thread.

   f. Call the `startRace` method in the `main` method and watch how the cars race


6. **Calculation of Results**

   a. To calculate the results of the race, it is necessary to synchronize the moment of crossing the finish line by all racers

   b. To do this, use `CountDownLatch`

   c. Create a new `CountDownLatch(n)` counter in the `Race` class in the main method, specifying the number of race participants in the constructor.

   d. Upgrade the `RaceCarRunnable` class. Add the `CountDownLatch` field to it and add it as a constructor parameter.

   e. In the `run` method of the `RaceCarRunnable` class, call the `latch.countDown();` at the time the car finishes.

   f. Add a "waiting point" (`latch.await();`) after calling the `startRace()` method.

   g. Display all finishing cars on the screen using the template "carName FINISHED!"


7. **Determination of the Winner**

   a. Add a static race start time field. In the `Race` class, define a public static field `startRaceTime` of type `AtomicLong`

   b. Initialize it with the value of the current system time at the time all threads start.

   c. Add field `long finishTime;` to the `RaceCarRunnable` class.

   d. Add a getter to this field.

   e. When the car crosses the finish line, calculate the race time. Current system time minus race start time (`finishTime`)

   f. Improve the output of the race results, add the arrival time of each car to the output of the result.

   g. Based on the known race results, determine the winner (whose `finishTime` is the shortest).

   h. Display the winner on the screen.


8. **Time Formatting***

   a. Create a static `String convertToTime(long time)` method that converts the race time from ms to a formatted time interval. Use `SimpleDateFormat`.
