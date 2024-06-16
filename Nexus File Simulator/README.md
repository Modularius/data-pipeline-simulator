=Nexus File Simulator=

Open a command terminal with current directory pointed at the repo.

To simulate a Nexus file, run each command in turn individually (to give time for it to complete):

1. `docker compose --profile=broker up -d`
2. `docker compose --profile=start up -d`
3. `docker compose --profile=writer up -d`
4. `docker compose --profile=start up -d`
5. `docker compose --profile=stop up -d`

The above commands are necessary to create the first simultation. To create subsequent files it is only necessary to run:

1. `docker compose --profile=start up -d`
2. `docker compose --profile=stop up -d`

To tear down the containers, run:
`docker compose --profile=all down`

== Simultation Settings ==

Open the `simulation_config.json` file.

=== Number of Frames to Simulate ===

To change the number of frames simulated, edit the `min` and `max` field in the line:

```json
"frames": { "interval": { "min": 0, "max": 1999 } },
```

These correspond to the first and last frame number simultated (inclusively), so `{ "min": 0, "max": 1999 }` will generate 2000 frames.

=== Number of Channels to Simulate ===

To change the number of channels simulated, edit the `min` and `max` field in the line:

```json
"source-type": { "aggregated-frame": { "channels": { "min": 0, "max": 999 } }},
```

These correspond to the first and last channel simultated (inclusively), so `{ "min": 0, "max": 999 }` will generate 1000 channel traces.

=== Number of Pulses to Simulate ===

To change the number of pulses simulated in a channel, edit the `"min": { "fixed-value": 0 }` and `"max": { "fixed-value": 100 }` field in the line:

```json
"num-pulses": { "random-type": "uniform", "min": { "fixed-value": 0 }, "max": { "fixed-value": 100 } },
```

These correspond to the minimum and maximum number of pulses generated in the trace, so `"min": { "fixed-value": 0 }, "max": { "fixed-value": 100 }` will randomly generate between 0 and 100 pulses.

N.B. The `"fixed-value"` syntax indicates that in more complex simulations, the upper and lower limits on the number of pulses can depend on frame number. This will be documented in the future.

=== Name of the Simulated Run ===

To change the Run Name, and hence the name of the generated file, edit the (possibly hidden) `.env` file.
Change the `RUN_NAME="SimulatedRun"` field to a whatever name you wish. Note this requires tearing down and restarting the `nexus-writer` service to take effect.
