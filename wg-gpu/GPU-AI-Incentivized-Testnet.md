# Akash Network - Incentivized Testnet for running AI workloads on GPU providers

Planned Timeline: May 30, 2023 - June 16, 2023

## Goals

- Validate Akash Network’s new GPU marketplace, prior to the upcoming planned mainnet upgrade.
- Validate Akash provider setup instructions for different types of K8s installations and Nvidia GPU types.
- Expand repository of open source container images and SDL (yaml) config files.
- Benchmark GPU performance against standard (Resnet and other) models, run on TensorFlow.
- Measure model GPU performance for inference on non-standard models, matching cost to performance.
- Generate content for marketing and education.
- Attract AI and ML enthusiasts/ experts to the Akash Network community.

## High Level Phased Plan

The high level plan will have 2 phases, with phase-1 tasks setting things up for phase-2 tasks

### Phase-1

Planned: May 29, 2023 through Jun 16, 2023

- Technical Level: Advanced
  - Knowledge of kubernetes, docker containers, and basics of AI model deployment and inference
  - Familiarity with Akash will help.
- Goals:
  - Validate provider setup.
  - Build GPU provider inventory for phase-2 testnet and mainnet.
  - Build benchmarking framework for phase-2 testnet and mainnet.
  - Build AI model SDL repository for phase-2 testnet and mainnet.
- Task Types:
  - Provider Setup Task (Advanced)
  - AI Model SDL Builder Task (Intermediate)
- Timeline & Incentives
  - This phase will run for 3 weeks.
  - The last week of phase-1 will overlap with phase-2.
  - Incentive for completing a task within first 2 weeks will be double that of doing so in the 3rd week (since phase-1 tasks feed into phase-2 so time is of essence).
  - Incentive amounts will be based on task types.

### Phase-2  

Planned: June 12, 2023 through Jun 16, 2023

- Technical Level: Intermediate to advanced
  - Familiarity with AI Model deployment and running inference
  - Familiarity with deploying workloads with SDL files using Akash Console or Cloudmos or Akash CLI will help.
- Goals:
  - Validate SDLs built by community for AI models
  - Test deployment of AI models on to GPU providers
  - Test deployment clients (Akash Console, Cloudmos, Akash CLI)
  - Run and Benchmark GPUs using the Jupyter Notebook + Tensorflow + Standard Models
  - Benchmark inference time for general AI Models
- Task Types:
  - AI Model Deployment & Benchmarking Task (Intermediate)
  - Tensorflow CNN benchmarking Task (Advanced)
- Timeline & Incentives
  - This phase will run for 1 week and overlap the last week of phase-1
  - Incentives for completing it earlier in the week, will be higher than doing so later in the week.
  - Specifics of timeline and incentives are called out in the individual tasks

## Task Types

There will be 4 task types, of varying incentives based on complexity

### Task-Type 1: Provider Setup Task (Advanced)

- Participants would need to setup an Akash provider with:
  - GPU Providers must contain at least one Nvidia GPU.
  - GPU Providers can be “heterogenous” but GPU provider nodes should be “homegenous”. I.e no mixing of GPU models.
  - GPU Provders at least 2 vCPUs
  - Off chip memory same or greater than the GPU on-chip memory.
  - The GPU should be one of the following Nvidia models: H100s, A100s, T4, V100, A10, A40, P4, K80, 4080s, 4090s, 3080s, 3090s.
  - Optionally (based on special request) RTX 2060, 2070, 2080, 2080Ti, GTX 1030, 1050, 1050Ti, 1060, 1070, 1070Ti, 1080, 1080Ti, 1630, 1650, 1660, 1660Ti.
  - Participants should follow the instructions documented in Akash documentation [here](https://docs.akash.network/other-resources/experimental/testnet/provider-build-with-gpu) for provider setup.
- Participants can source the GPU from anywhere they like - could be their own, could be from a datacenter, could even be a cloud provider.
- Participants may set up and manage kubernetes cluster using their preferred method.
- Participants should report status of their efforts (like “done setting up K8s cluster, used my on prem infrastructure” and “provider ready for signing”) so that we can watch progress and benchmark the time it takes for the average user to set up a provider.
- Participants are encouraged to provide feedback about the overall process (pain points, documentation issues, bugs, ideas for improvement etc).
- **Timeline**: Participants will be given 3 weeks to complete the task but the incentive for completing the task in the 2nd week will be 50% of the max (the first week incentive) and of completing in the 3rd week will be 25% of the max (the first week incentive).
- **Incentive**: To be communicated soon but it will offset some portion of the cost of running the provider for the duration of the testnet.

### Task Type 2: AI Model SDL Builder Task (Intermediate)

- Participants will be required to build Akash SDL configs (and container images, if needed) for specific AI models or applications and commit them to the open source code repository at https://github.com/akash-network/awesome-akash. Examples of such SDL configs are:
  - https://github.com/akash-network/awesome-akash/tree/master/alpaca-cpp
  - https://github.com/akash-network/awesome-akash/tree/master/ai-chat-app
  - https://github.com/akash-network/awesome-akash/tree/master/stable-diffusion-ui
- Additional documentation on how to build SDLs is located at https://docs.akash.network/readme/stack-definition-language andhttps://docs.akash.network/other-resources/experimental/testnet/provider-build-with-gpu/gpu-test-deployments#example-gpu-sdl.  
- Participants are encouraged to deploy some existing SDLs from the awesome-akash repository using any deployment client (Console, Cloudmos or Akash CLI) to familiarize themselves with the process.
- Participants are encouraged to build SDLs for AI models from this google sheet that do not already have an SDL yaml file in the awesome-akash repository. If the participant already has a container image for some other AI model, not listed in this sheet, they are welcome to use that as well.
- Participants must submit a PR into the awesome-akash repository and confirm deployment of the model on any of the available GPU providers and post log output and/ or screen recording of it. Participants are encouraged to share this on social media as well.
- **Timeline**: Participants will be given 3 weeks to complete the task but the incentive for completing the task in the 2nd week will be 50% of the max (the first week incentive) and of completing in the 3rd week will be 25% of the max (the first week incentive).
- **Incentive**: To be communicated soon.

### Task Type 3: TensorFlow CNN benchmarking Task (Advanced)

- Participants would run the TensorFlow(TF) benchmark tests on Akash GPUs:
  - https://github.com/tensorflow/benchmarks (general framework)
  - https://github.com/tensorflow/benchmarks/tree/master/scripts/tf_cnn_benchmarks (old/ unsupported models but reference for set up)
  - https://github.com/tensorflow/models/tree/master/official (new/ supported models)
- A task would consist of picking one of the models from https://github.com/tensorflow/models/tree/master/official and running it across multiple GPUs (sheet with combinations TBD).
- Participants would run an instance of Jupyter Notebook on the specific Akash provider that has the GPU they plan to benchmark and then run the model and dataset using the Jupyter Notebook. Here is the SDL for running a [Jupyter notebook](https://github.com/akash-network/awesome-akash/blob/master/tensorflow-jupyter-mnist/deploy.yaml). 
- Participants would report results in the format specified (TBD).
- Participants are allowed to deploy a model that has already been tested and reported the maximum number (5) times but we will only award incentives to the first 5 successful, unique tests completed.
- **Timeline**: Participants will be given 1 week to complete the task.
- **Incentive**: Participants will receive xx AKT for completing the task and an additional xx AKT for sharing the deployment on social (Twitter, Linkedin and/ or YouTube)

### Task Type 4: AI Model Deployment & Benchmarking Task (Intermediate)

- Participants would pick models from the [models google sheet](https://docs.google.com/spreadsheets/d/1szqG16JMhodaKWX7YkT_gLeocgfiglssIsw5Xy-653Q/edit#gid=598527902).
- For each model, they would attempt to deploy on any/ all available providers and record whether they succeeded or not and record specific metrics as called out in the benchmarking sheet (TBD)
- Participants may use any preferred client (Akash Console, Cloudmos or Akash CLI) to complete the task
- Participants will be required to share a video of their deployment on social media and are encouraged to create a video on youtube, if they are a content creator.
- Participants will be required to submit numbers for benchmarking times in the format provided (TBD).
- **Timeline**: Participants will be given 1 week to complete the task.
- **Incentive**: Participants will receive xx AKT for completing the task and an additional xx AKT for sharing the deployment on social (Twitter, LinkedIn and/ or YouTube).
