# UAV-SIM-STARTER

### From Zero to Your First Simulated Drone Flight

A beginner-friendly, step-by-step guide to setting up a drone simulation environment using **ArduPilot SITL, ROS, and Gazebo**.

Getting started with drone simulation can be surprisingly frustrating. Between operating system compatibility, missing dependencies, conflicting software versions, and configuration errors, getting your first drone airborne can involve more troubleshooting than expected.

This repository aims to make that process easier.

It documents the tools, configurations, and troubleshooting steps needed to build a working drone simulation environment, starting with a single drone and eventually extending to multiple independently controlled UAVs.

## What You'll Learn

- Setting up Ubuntu for robotics development.
- Understanding how ROS, Gazebo, ArduPilot, and MAVLink work together.
- Installing and configuring ArduPilot SITL.
- Launching and controlling a simulated drone.
- Visualising onboard camera feeds and telemetry.
- Running multiple independent drones in the same simulation.
- Diagnosing common installation and configuration errors.

## Technology Stack

| Technology | Purpose |
|---|---|
| Ubuntu 20.04 | Development environment |
| ROS Noetic | Robotics middleware |
| Gazebo 11 | Physics and 3D simulation |
| ArduPilot SITL | Simulated flight controller |
| MAVLink / MAVProxy | Drone communication and control |
| MAVROS | Communication between ROS and MAVLink |
| QGroundControl | Ground control station |

> **Compatibility Note:** This guide documents a legacy, version-specific environment. ROS Noetic reached end of life in May 2025. This setup is intended for learning and reproducing the documented simulation environment, rather than as a recommendation for new production deployments.
>
> The complete setup has not been verified across all hardware architectures or current software releases.

## Documentation

The repository is being organised into the following guides:

1. **Ubuntu Setup:** Preparing the development environment.
2. **Understanding the Stack:** How the simulation components communicate.
3. **Installation:** Installing and configuring the required tools.
4. **First Flight:** Launching and controlling your first simulated drone.
5. **Multi-Drone Simulation:** Running two independently controlled UAVs.
6. **Troubleshooting:** Common problems and their solutions.

Documentation will be added progressively.

## Expected Outcome

By completing the single-drone setup, you should be able to:

- Launch a simulated drone in Gazebo.
- Control its flight using ArduPilot SITL and MAVProxy.
- Visualise its camera feed through ROS.
- Connect QGroundControl for telemetry and waypoint missions.

The multi-drone guide extends this environment to two independently controlled simulated UAVs with separate camera feeds.

## Why This Repository?

This repository grew out of my experience setting up UAV simulation environments during my exploration of drone autonomy.

I repeatedly encountered compatibility issues, dependency conflicts, and configuration problems while working across different environments.

Rather than keeping those solutions scattered across notes, I wanted to organise them into a resource that other beginners could follow.

The goal isn't just to provide installation commands, but to explain **what each component does, why it's required, and how to identify problems when something breaks.**

## Contributions

Found an outdated command, a missing dependency, or a clearer way to explain something?

Issues and suggestions are welcome.

---

**Maintained by Mohammad Talha**

Built for students, robotics enthusiasts, and anyone curious about UAV simulation.
