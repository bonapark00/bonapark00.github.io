---
layout: page
title: Golden Time - 
# description: with background image
img: assets/img/projects/golden_time/
importance: 1
category: work
related_publications: true
---

<h1 align="center">Golden Time - Wear OS⌚</h1>
<h3 align="center">For 2023 Google Developers Solution Challenge</h3>
<p align="center">
  <img src="https://user-images.githubusercontent.com/11978494/228843932-c59e03fb-d4e7-458d-a548-58e80583a7ea.png" alt="icon" width="250" height="250">
</p>

## Overview

*Golden Time* is a service helping rescuers to save the patient with the proper manual. By sharing the patient's manual to nearby people when an emergency occurs, it shortens rescuer's hesitating time and prevents some critical dangers such as WRONG ACTIONs. And this is the main application of Golden Time running in Android. You can check out other components of our service such as [Golden Time - Backend](https://github.com/gdsc-ys/golden-time-backend) and [Golden Time - WearOS](https://github.com/gdsc-ys/golden-time-wearos)

The overall process is as follows.
1. Register a disease with related manuals.
2. If SOS triggered (by manually, irregular heart rate detection, or fall detection), send the patient's medical ID and manauls to nearby people.
3. People around the patient receive a message containing the patient's medical ID and a manual registered by the patient.
4. Automatically calling to 911, the rescuers help the patient to be saved with the proper manual.

In addition to the main flow, users can read and study various diseases with an article tab.
With our wearable application [WearOS for Golden Time](https://github.com/gdsc-ys/golden-time-wearos), the patient can monitor his or her heart rates and trigger an emergency SOS automatically if it detects an irregular heart rate or a falling activity.

## Our goals

| Good Health and Well-being | Quality Education | Reduced Inequality |
|:-:|:-:|:-:|
| <img width="50%" src="https://user-images.githubusercontent.com/11978494/229120095-200494e8-a916-4387-bee3-70477d2b4824.png"> | <img width="50%" src="https://user-images.githubusercontent.com/11978494/229120393-90b52bc9-94e1-4c8b-b709-25d8c4dfe423.png"> | <img width="50%" src="https://user-images.githubusercontent.com/11978494/229120495-43c49966-c735-4ebd-97f5-0d92ce349f5f.png"> |

## High-level architecture

![Solution Challenge - High level architecture](https://user-images.githubusercontent.com/11978494/229120978-77f4b040-933d-42a6-880c-fd1e2fd4f0bb.png)

## WearOS
Wear OS for Golden Time has been made to assist an Mobile application for Golden Time. It monitors user's body condition and send alert to the application in case of an emergency. We took advantage of high quality data from **[Health Services](https://developer.android.com/training/wearables/health-services)**.

Our Wear OS continuously measures user's **heart rate** and detects **falling activity**. If the heart rate is outside of the normal range(40-10bpm) or fall activity is detected by Health Services, it finds the user is in emergent situation.

Wear device and a handheld communicate using [MessageClient](https://developer.android.com/training/wearables/data/messages). If a MessageClient listener on a mobile application recieves a message, new activity starts on the mobile device and emergency is handeled.

## Screenshots

![Screenshot_20230402_175812_framed](https://user-images.githubusercontent.com/11978494/229343034-d82c56eb-a26c-45ee-8e00-318b7b4eca73.png)

## Features
The Wear OS for Golden Time lets you:
- Measure your heart rate
- Detect when you have fallen
- Send emergency message to Android application

## Technologies
- Andorid Studio
- Kotlin
- MVVM architecture
- Health Services



## Getting Started
### Prerequisites
- Min SDK version: 30
- Target SDK version: 32
### Clone
Clone this repo to your local machine using:

```
git clone https://github.com/gdsc-ys/golden-time-wearos/
```
## Permissions
On Android, Wear OS for Golden Time requires the following permissions:
- Sensors
- Physical activities

