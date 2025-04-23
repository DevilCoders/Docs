# ReConf-Juggler aggregates builder/deployer sandbox task

## Goal

Provide continuous delivery for aggegates builders based on
[ReConf-Juggler](https://a.yandex-team.ru/arc/trunk/arcadia/infra/reconf_juggler/)

## Usage

Typical workflow is build -> approve (release) -> deploy

This task works in two modes:

1. Deploy arbitrary aggregates (when defined resource ID with aggregates and
   Juggler OAuth creds).

2. Build aggregates (when defined builder path in arcadia). Release task in
   this mode will cause aggregates deploy to Juggler (Juggler OAuth creds
   should be defined also in this case).

## StarTrek integration

To be able to recieve notifications to tickets, StarTrek creds should be
provided.
