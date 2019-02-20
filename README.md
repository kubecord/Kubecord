# Kubecord
Meta-repository for Kubecord: a scalable, microservice-based Discord bot framework.

![Discord](https://img.shields.io/discord/546429690198622219.svg)
![GitHub](https://img.shields.io/github/license/kubecord/Kubecord.svg)

## What is Kubecord?
Kubecord is a framework for creating Discord bots that are scalable, light-weight, and self-healing.  The focus is to target Kubernetes as a platform, but we will provide instructions and tooling to deploy to other environments as well.

![Kubecord](/images/kubecord.png)

## I'm currently using X Discord library, what makes you better?
Classical API libraries don't scale well, and some have issues with potential stack overflows, and memory leaks.  As your bot grows, you'll start to notice the pain of running and scaling larger bots using the typical library.  Discord requires sharding after a certain number of guilds, and require that you maintain at most 2500 guilds per shard.  This is to reduce the load on Discords end, but can lead to some interesting situations where the largest guilds your bot serves are all on one shard, making automated scaling systems inefficient.  Kubecord is designed to scale your bot based on load, not arbitrary guild counts.  We also make it easy to break your bot apart into smaller logical components that each scale on their own, saving you a lot in compute resources.

Furthermore, separating different components of the bot into smaller peices will prevent poor performance or large load on one system, for example: auto-moderation, from affecting the rest of the bot or its ability to consume events from Discord.

We also take care of a lot of the struggles of IPC and coordinating state data between multiple shards for you.  So you will be able to access external emojis from any guild your bot is in 😉

## How does it work?
We provide Kubernetes deployment files, and a docker-compose file to make it easy for you to deploy the framework.  The base framework consists of 4 components: a websocket handler, a rest ratelimit manager, [NATS](https://nats.io), and [redis](https://redis.io).  It is then up to your to use one of our worker libraries to build your bot logic, and deploy that to connect to the rest of the framework and start serving requests.  Without workers, Kubecord will effectively just maintain a state cache for you.

![Kubecord diagram](/images/kubecord-diagram.png)

## Cool, how can I get started?
At this time, the project is still in very active development, we are working with a few larger bot developers to integrate and test this system before we provide public releases. Stay tuned, and join us on Discord to discuss the project and recieve updates!
