# weather_icons

A Flutter library for using [Weather Icons](https://erikflowers.github.io/weather-icons/).

[![CircleCI branch](https://img.shields.io/circleci/project/github/worldturtlemedia/weather_icons/master.svg?label=release%20build)](https://circleci.com/gh/worldturtlemedia/weather_icons) ![GitHub](https://img.shields.io/github/license/worldturtlemedia/weather_icons.svg) [![Coverage Status](https://coveralls.io/repos/github/worldturtlemedia/weather_icons/badge.svg?branch=master)](https://coveralls.io/github/worldturtlemedia/weather_icons?branch=master)

[![Pub](https://img.shields.io/pub/v/weather_icons.svg?style=flat-square)](https://pub.dartlang.org/packages/weather_icons) [![GitHub release](https://img.shields.io/github/release/worldturtlemedia/weather_icons.svg?label=gh-release)](https://github.com/worldturtlemedia/weather_icons/releases) [![GitHub commits since latest release](https://img.shields.io/github/commits-since/worldturtlemedia/weather_icons/latest/master.svg)](https://github.com/worldturtlemedia/weather_icons/commits/master)

**Note:** All of the icon data is auto-generated based on the latest release of [Weather Icons](https://github.com/erikflowers/weather-icons/releases).

## Installation

Add the dependency to your `pubspec.yaml`

```yaml
dependencies:
  weather_icons: 1.0.x # Use the latest version
```

## Usage

The library exposes all of the [Weather Icons](https://erikflowers.github.io/weather-icons/) as `IconData`. The naming convention is the same as the CSS names, minus the `wi-`, and all dashes replaced with underscores. It was named this way to match the default `Icons` class.

If you know which icon you need, you can use the provided constant icons. If you need a dynamic icon see below.

```dart
import 'package:flutter/material.dart';
import 'package:weather_icons/weather_icons.dart';

class MyWidget extends StatelessWidget {
  Widget build(BuildContext context) {
    return Icon(
      icon: BoxedIcon(WeatherIcons.day_sunny),
      onPressed: () {
          print("Foo");
      }
     );
  }
}
```

### Note

Because of how the icons exist in the font file, there will be some display issues when using a standard `Icon` widget. The icon will draw outside of its boundaries causing issues with layouts and padding, etc.

You can see an example of this in the `example/` application.

In order to overcome this, the library exposes a widget called `BoxedIcon`. Which puts the icon into a 'box' which properly sets its height, and width. Preventing any of the out of boundary drawing.

Anywhere you can use `Icon`, you can swap it out for `BoxedIcon`.

```dart
class MyWidget extends StatelessWidget {
  Widget build(BuildContext context) {
    return Icon(
      icon: BoxedIcon(WeatherIcons.day_sunny),
      onPressed: () {}
     );
  }
}
```

See [`weather_icons_g.dart`](https://github.com/worldturtlemedia/weather_icons/blob/master/lib/src/weather_icons_g.dart) for all of the icons.

### Dynamic

If you need a dynamic icon at run-time, then you can use the included helper function for converting from the CSS style name to a `IconData`.

```dart
import 'package:flutter/material.dart';
import 'package:weather_icons/weather_icons.dart';

class WeatherDisplay extends StatelessWidget {
  final String weatherCode;

  WeatherDisplay(this.weatherCode);

  Widget build(BuildContext context) {
    return Container(
      child: Column(
        children: [
          BoxedIcon(
            WeatherIcons.fromString(
                weatherCode,
                // Fallback is optional, throws if not found, and not supplied.
                fallback: WeatherIcons.na
            ),
          ),
          Text("Icon for '$weatherCode'"),
        ],
      ),
    );
  }
}
```

### Wind Direction

The wind icon is a special icon, as it is one single icon value that is then rotated using CSS. To achieve a similar functionality you can use the `WindIcon` class.

The `WindIcon`'s always use `BoxedIcon`.

**Note:** This means that `WeatherIcons.wind` will always be the North facing icon.

```dart
import 'package:flutter/material.dart';
import 'package:weather_icons/weather_icons.dart';

class EastlyWindWidget extends StatelessWidget {
  Widget build(BuildContext context) {
    return IconButton(
      // Display a Wind icon facing towards east
      icon: WindIcon.towards_e,
      onPressed: () { ... }
     );
  }
}
```

Since the [Weather Icons](https://github.com/erikflowers/weather-icons) support both 'towards' and 'from' wind directions, this library does as well.

### Dynamic Wind Direction

Just like the weather above, if your wind direction is dynamic you can create your own `WindIcon`.

```dart
import 'package:flutter/material.dart';
import 'package:weather_icons/weather_icons.dart';

class WindDirectionDisplay extends StatelessWidget {
  final double windDirectionDegree;

  WindDirectionDisplay(this.windDirectionDegree);

  Widget build(BuildContext context) {
    return Container(
      child: Column(
        children: [
          WindIcon(degree: windDirectionDegree),
          Text("Icon for wind @ $windDirectionDegree°"),
        ],
      ),
    );
  }
}
```

**Note:** The degree must be within the degrees of a compass/circle, so 0-360.

## Time icons

`weather_icons` also includes a helper for displaying the time icons.

```dart
// Manual hour
IconButton(
  icon: BoxedIcon(TimeIcon.iconFromHour(3)),
  onPressed: () { print("Displaying the third hour!"); }
);

// Using a DateTime instance
IconButton(
  icon: BoxedIcon(TimeIcon.iconFromDate(DateTime.now())),
  onPressed: () { print("Current hour"); }
);

// Creating your own Icon
BoxedIcon(
  icon: TimeIcon.fromHour(3),
  size: 60,
)

// Also using a DateTime
BoxedIcon(
  icon: TimeIcon.fromDate(DateTime.now()),
  size: 60,
)
```

## Example

A full example can be found in the [example](https://github.com/worldturtlemedia/weather_icons/tree/master/example) folder.

## TODO

- Add support for the weather service mappings [here](https://erikflowers.github.io/weather-icons/api-list.html)

## Contributing

See [CONTRIBUTING](https://github.com/worldturtlemedia/weather_icons/blob/master/CONTRIBUTING.md)

## License

```text
MIT License

Copyright (c) 2019 WorldTurtleMedia

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

```
