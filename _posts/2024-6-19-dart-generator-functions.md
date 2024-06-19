---
layout: post
title: Dart Generator Functions
tags: rails ruby
---



### Why

When you need to lazily produce a sequence of values, consider using a generator function. Dart supports both `synchronous` and `asynchronous` generators.

`Lazily produce` means generating next value when requested. The request action can refer to calling [Iterator<E>.moveNext()](https://api.dart.dev/stable/3.4.4/dart-core/Iterator/moveNext.html) for synchronous geneartor, or consuming emitted values from stream by `await for` or `listen to`.


### How

- `*sync`: A generator with `Iterable` as output.
- `*async`: A generator with `Stream` as output.
- `yield`: Drop a value to the ouput tunnel. The function pauses execution at each "yield" until next value is requested. It's like return, but does not teminate the function. Also the function automatically pauses at a yield statement while the steam subscription is paused (or iterator is not longer called moveNext()).
- `*yield`: Delegate to another generator, which means current geneartor stops until the delegated one stop producing values.




### What

- One of good use case for `Synchrnous Generators` is to calculate a sequence of values which are computation-heavy. Due to generator's laziness nature, we can do this in a memory-efficient manner.

    ```
    void main() {
        // Create an instance of the generator function
        Iterable<int> numbers = generateNumbers(5);

        // Iterate over the generated numbers and print them
        for (int number in numbers) {
            print(number);
        }
    }

    // A synchronous generator function that generates numbers from 0 to n-1
    Iterable<int> generateNumbers(int n) sync* {
        for (int i = 0; i < n; i++) {
            yield i; // Pause and return the current value of i
        }
    }
    ```

- `Asynchrnous Generators` enable use to wait during the process of delivering a value. It's not that different from the `synchrnous` one. Remeber: The key takeaway is `laziness`.

    ```
    import 'dart:async';

    void main() async {
        // List of sensor IDs
        List<String> sensorIds = ['sensor1', 'sensor2', 'sensor3'];

        // Process data from all sensors
        await processSensorData(sensorIds);
    }

    // Simulate a sensor data stream with temperature readings
    Stream<int> simulateSensorData(String sensorId) async* {
        for (int i = 0; i < 10; i++) {
            await Future.delayed(Duration(seconds: 1)); // Simulate delay
            yield (20 + i); // Simulate a temperature reading
        }
    }

    Future<void> processSensorData(List<String> sensorIds) async {
        // Create a list of sensor data streams
        List<Stream<int>> streams = sensorIds.map(simulateSensorData).toList();

        // Merge all sensor data streams into a single stream
        Stream<int> mergedStream = StreamGroup.merge(streams);

        // Process each sensor reading as it arrives
        await for (int reading in mergedStream) {
            print('Received sensor reading: $reading');
            // Perform any necessary processing here
        }
    }

    ```




### Where


### When



### Who