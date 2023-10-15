# R-ZWEI-Kickers-Code-Release-2023
This is the 2023 code release of the RoboCup-SPL team R-ZWEI Kickers. This README-file shortly illustrates the structure of our codebase.

## Some notes before cloning

Please note that **before** you clone this repository on Windows, execute:
```
git config --global core.autocrlf input
git config --global core.eol lf
```

As this repository uses submodules, it must be cloned using `git clone --recursive`. Downloading the release as `zip` or `tar.gz` does not work.

## B-Human Code Release

Since our team is still very new in the league and our numbers are pretty small we didn't start everything from scratch. Our code is based on the official 2021 B-Human code release. Documentation for it can be found in their [public wiki](https://wiki.b-human.de/coderelease2021/).

Previous of their code releases are tagged with "coderelease&lt;year&gt;", where &lt;year&gt; is the year in which the code was released (starting with 2013).

## Changes

Since starting working on BHuman's 2021 code release the team has added some features to the codebase, such as:

### Behaviour Control

#### Behaviour Cards

The behavior of the robots was configured by writing cards in BHuman's Skills and Cards system in order to configure the robots' behaviours within different gameplay situations. 

Overall our behaviour works with dynamic role assignment, e.g.
- a defender substitutes the goalie if the goalie is unavailable
- play with less strikers and more defenders when in the lead
- play defensively if a lot of team members are out of commission at a given moment in time

#### DefaultPoseProvider

A provider that provides our robots with their respective default pose on whatever field they are deployed in. For our purposes two more field setups were configured:
- HalfField: The robots are playing on one half of the field
- Labor: The robots are deployed on a smaller than usual field that fits inside our lab room at the university

These field configurations were necessary to account for the fact, that often (especially in the very beginnings of our teams existence) we simply did not have the room available in order to setup a proper field with the right measurements. 

#### ShotPredictor

The behaviour of a robot playing as striker uses this piece of behaviour in order to determine whether or not to take a shot at the goal or not. The predictor provides the bot with a probabilistic value and given a certain threshold and using this value the bot then decides whether or not to take a shot or not. 

### Communication

The existing communication modules were updated to account for the message restrictions the league has put in place for the 2023 season. Other than that, there was an overhaul of the whole communication system.

***Important Note**: Unfortunately the communication overhaul breaks working with the simulator at the time of this release since it makes all the robots huddle into one spot. However, when deploying on the robots in a real life field, this issue does not occur.
The issue stems from the fact, that the simulator saves space by using only one instance of shared information amongst robots while in real life each robot of course has their own instance/copy of that. We're currently investigating and fixing the issue.*

### Shared

We've added a module for shared information that provides the team with strategically relevant information.

## Adjustments

Of course we also had to adjust a lot of stuff for our purposes, e.g.
- we had to add configurations for each of out bots
- we had to configure different field sizes to deploy in
- we have made adjustments to most modules in order to make them work with our strategic implementations and added features, prominently but not exclusively in:
    - different locators and WhistleDetection
    - Perception (e.g. Jersey Detection)
    - Communication