# Делаем севрис с апи за которым скрываем детали реализации

## Status

accepted

## Context

Доступ к фин статистики через апи статиста имеет недостатки 
 - размазана ответственность за сервис, потребители будут ходить с вопросами и багами 
   и к нам и к ним, это усложнит комункации между командами
 - Мы завязанны на апи и возможности статиста

## Decision

Делаем сервис с апи, через который все потребители будут получать статистику 

## Consequences

Потребители работают с нашим апи, в случае проблем приходят сразу к нам
Мы скрываем детали реализации статистики, формируем апи такое какое удобно нам и потребителям
