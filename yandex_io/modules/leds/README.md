# Observers for LED Animation

Led animation is a vendor part of work.
Quasar has its own base implementation for LED animations. It consists of LedManager and LedController.

## LedController
LedController is an interface for vendor specific implementations.
This interface has simple method ```drawFrame``` that should draw a frame on leds

## LedManager
LedManagerBase is a class that provide more simple interface between user and LedController.
LedManagerBase works with Patterns that define each led animation.

## Observers
This directory contains implementations for YandexIO observers that can draw simple led animations (which depend on Observer)

