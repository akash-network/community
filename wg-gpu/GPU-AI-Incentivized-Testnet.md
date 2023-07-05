# Akash Network - Incentivized Testnet for running AI workloads on GPU providers

Tentative Timeline (may be delayed by a week): June 20, 2023 to July 11, 2023 

## Goals

- Validate Akash Network’s new GPU marketplace, prior to the upcoming planned mainnet upgrade.
- Validate Akash provider setup instructions for different types of K8s installations and Nvidia GPU types.
- Expand repository of open source container images and SDL (yaml) config files.
- Benchmark GPU performance against standard (Resnet and other) models, run on TensorFlow.
- Measure model GPU performance for inference on non-standard models, matching cost to performance.
- Generate content for marketing and education.
- Attract AI and ML enthusiasts/ experts to the Akash Network community.

## High Level Phased Plan

The high level plan will have 2 phases, with phase-1 tasks setting things up for phase-2 tasks. The phases and tasks are detailed below and the incentives are detailed [here](https://docs.google.com/spreadsheets/d/1z_2Fx6u7U48LrxNj8IaDKjlnp84KOEgMb_hJw-Q1TjQ/edit#gid=2126550797).

### Phase-1

Planned: June 20, 2023 to July 11, 2023

- Technical Level: Advanced
  - Knowledge of kubernetes, docker containers, and basics of AI model deployment and inference.
  - Familiarity with Akash will help.
- Goals:
  - Validate provider setup.
  - Build GPU provider inventory for phase-2 testnet and mainnet.
  - Build AI model SDL repository for phase-2 testnet and mainnet.
- Task Types:
  - Provider Setup Task (Advanced) - Task Type 1 below.
  - AI Model SDL Builder Task (Intermediate) - Task Type 2 below.
  - In addition there will be bonus incentives for sharing your work on Twitter and YouTube as called out in Task Types 5 & 6 below.
- Timeline & Incentives
  - This phase will run for 3 weeks.
  - The last week of phase-1 will overlap with phase-2.
  - Incentive for completing tasks earlier will be higher than those for completing them later during the testnet (since phase-1 tasks feed into phase-2, so time is of essence).
  - Incentive amounts will base based on task types as described below and detailed [here](https://docs.google.com/spreadsheets/d/1z_2Fx6u7U48LrxNj8IaDKjlnp84KOEgMb_hJw-Q1TjQ/edit#gid=2126550797).

### Phase-2  

Planned (may be delayed by a week): July 5, 2023 to July 11, 2023

- Technical Level: Intermediate to Advanced
  - Familiarity with AI Model deployment and running inference.
  - Familiarity with deploying workloads with SDL files using Akash Console or Cloudmos or Akash CLI will help.
- Goals:
  - Validate SDLs built by community for AI models.
  - Test deployment of AI models on to GPU providers.
  - Test deployment clients (Akash Console, Cloudmos, Akash CLI).
  - Run and Benchmark GPUs using the Jupyter Notebook + Tensorflow + Standard Models.
  - Benchmark inference time for general AI Models.
- Task Types:
  - Tensorflow CNN benchmarking Task (Advanced) - Task Type 3 below.
  - AI Model Deployment Task (Intermediate) - Task Type 4 below.

  - In addition there will be bonus incentives for sharing your work on Twitter and YouTube as called out in Task Types 5 & 6 below.
- Timeline & Incentives:
  - This phase will run for 1 week and overlap the last week of phase-1.
  - Incentives for completing it earlier in the week, will be higher than doing so later in the week.
  - Specifics of timeline and incentives are called out in the individual tasks and detailed [here](https://docs.google.com/spreadsheets/d/1z_2Fx6u7U48LrxNj8IaDKjlnp84KOEgMb_hJw-Q1TjQ/edit#gid=2126550797).

## Tasks

There will be 6 task types, with varying incentives based on the complexity of the task.

### Task Type 1: Provider Setup Task (Advanced)

- Participants would need to setup an Akash provider with:
  - At least one Nvidia GPU.
  - GPU Providers can be “heterogenous” but GPU provider nodes should be “homegenous”. I.e no mixing of GPU models.
  - At least 2 vCPUs.
  - Off chip memory same or greater than the GPU on-chip memory.
  - The GPU should be one of the following Nvidia models: H100, A100, V100, P100, A40, A10, P4, K80, T4, 4090, 4080, 3090Ti, 3090, 3080Ti, 3080, 3060Ti.
  - Optionally (based on special request/ approval) RTX 2060, 2070, 2080, 2080Ti, GTX 1030, 1050, 1050Ti, 1060, 1070, 1070Ti, 1080, 1080Ti, 1630, 1650, 1660, 1660Ti.
  - Participants should follow the instructions documented in Akash documentation [here](https://docs.akash.network/other-resources/experimental/testnet/provider-build-with-gpu) for provider setup.
- Participants can source the GPU from anywhere they like - could be their own, could be from a datacenter, could even be a cloud provider.
- Participants may set up and manage kubernetes cluster using their preferred method.
- Participants should report status of their efforts (like “done setting up K8s cluster, used my on prem infrastructure” and “provider ready for signing”) so that we can watch progress and benchmark the time it takes for the average user to set up a provider.
- Participants are encouraged to provide feedback about the overall process (pain points, documentation issues, bugs, ideas for improvement etc).
- Participants will be required to submit a typeform form when they complete the challenge. Challenge submission form will require:
  - Screen shot of a deployment on the provider and with the logs pane shown in the screen shot.  We will supply a SDL that must be used for this first deployment and that SDL will log their GPU type.
  - Timestamp of successful build: The time that the form was submitted will be used for this.
- The Overclock Labs team and Akash community will also verify that the provider was running for the entire duration of the testnet, while determining eligibility for the reward.
- **Timeline**: Participants will be given 3 weeks to complete the task but the incentive for completing the task in the 2nd week will be 50% of the max (the first week incentive) and of completing in the 3rd week will be 25% of the max (the first week incentive).
- **Incentive**: As detailed [here](https://docs.google.com/spreadsheets/d/1z_2Fx6u7U48LrxNj8IaDKjlnp84KOEgMb_hJw-Q1TjQ/edit#gid=2126550797). Note that Overclock Labs will be incentivizing a total of 30 GPUs of which at least 10 must be "Data Center Grade" GPUs (H100, A100, V100, P100, A40, A10, P4, K80, T4).

### Task Type 2: AI Model SDL Builder Task (Intermediate)

- Participants will be required to build Akash SDL configs (and container images, if needed) for specific AI models or applications and commit them to the open source code repository at https://github.com/akash-network/awesome-akash. Examples of such SDL configs are:
  - https://github.com/akash-network/awesome-akash/tree/master/alpaca-cpp
  - https://github.com/akash-network/awesome-akash/tree/master/ai-chat-app
  - https://github.com/akash-network/awesome-akash/tree/master/stable-diffusion-ui
- Additional documentation on how to build SDLs is located at https://docs.akash.network/readme/stack-definition-language and https://docs.akash.network/other-resources/experimental/testnet/provider-build-with-gpu/gpu-test-deployments#example-gpu-sdl.  
- Participants are encouraged to deploy some existing SDLs from the awesome-akash repository using any deployment client (Akash Console, Cloudmos or Akash CLI) to familiarize themselves with the process.
- Participants are encouraged to build SDLs for AI models from this google sheet that do not already have an SDL yaml file in the awesome-akash repository. If the participant already has a container image for some other AI model, not listed in this [sheet](https://docs.google.com/spreadsheets/d/1szqG16JMhodaKWX7YkT_gLeocgfiglssIsw5Xy-653Q/edit#gid=598527902), they are welcome to use that as well.
- Participants must submit a PR into the awesome-akash repository, and confirm deployment of the model on any of the available GPU providers and post log output and/ or screen recording of it. The SDL needs to inlcude a user interace (UI), so once deployed, users can interact with the model. Participants are encouraged to share this on social media as well.
  - Detailed description including model deployed and requirements for the model.
  - PR must include a video of a web interface with a prompt that the AI model will act on.
  - PLEASE TEARDOWN DEPLOYMENT AFTER VIDEO IS CREATED.
- Participants will be required to submit a typeform form when they complete the challenge. Challenge submission form will require:
  - Link to PR submitted to awesome-akash repository.
  - Timestamp of submission: The form submission timestamp will be used for this.
- **Timeline**: Participants will be given 2 weeks to complete the task but the incentive for completing the task in the 2nd week will be 50% of the max (the first week incentive).
- **Incentive**: As detailed [here](https://docs.google.com/spreadsheets/d/1z_2Fx6u7U48LrxNj8IaDKjlnp84KOEgMb_hJw-Q1TjQ/edit#gid=2126550797).

### Task Type 3: Pytorch / TensorFlow CNN benchmarking Task (Advanced)

- Participants would run benchmark tests on Akash GPUs, using either Pytorch or TensorFlow(TF) :
  - ***Pytorch Reference:*** 
    - https://github.com/pytorch/benchmark/tree/main (general framework)
    - https://github.com/pytorch/benchmark/tree/main/torchbenchmark/models (supported models).
      
  - ***TensorFlow Reference:***
    - https://github.com/tensorflow/benchmarks (general framework).
    - https://github.com/tensorflow/benchmarks/tree/master/scripts/tf_cnn_benchmarks (old / unsupported models but reference for set up).
    - https://github.com/tensorflow/models/tree/master/official (new / supported models).
      
    - A task would consist of picking one of the models from https://github.com/tensorflow/models/tree/master/official and running it across multiple GPUs (sheet with combinations TBD).
    - Participants would run an instance of Jupyter Notebook on the specific Akash provider that has the GPU they plan to benchmark and then run the model and dataset using the Jupyter Notebook. Here is an SDL for running a Jupyter notebook https://github.com/akash-network/awesome-akash/blob/master/tensorflow-jupyter-mnist/deploy.yaml. We also have another in the works for Pytorch https://github.com/akash-network/awesome-akash/pull/388

- **Timeline**: Participants will have ***6*** days to complete the task, in order to be eligible to receive reward, with rewards highest for those completing it on the first day of the week.
- **Incentive**: As detailed [here](https://docs.google.com/spreadsheets/d/1z_2Fx6u7U48LrxNj8IaDKjlnp84KOEgMb_hJw-Q1TjQ/edit#gid=2126550797)
  - Participants are allowed to deploy a model that has already been tested and reported the maximum number (5) times but we will only award incentives to the first 5 successful, unique tests completed.

### Task Type 4: AI Model Deployment Task (Intermediate)

- Participants would pick models from [awesome-akash](https://github.com/akash-network/awesome-akash#ai).
- For each model, they would attempt to deploy on any ***3*** different available providers.
- Participants may use any preferred client (Akash Console, Cloudmos or Akash CLI) to complete the task.
- Participants are encouraged to share their deployments on Twitter and YouTube and a limited number will receive an incentive as called out in Tasks 5 & 6 below.
- Participants will be required to submit a typeform form when they complete the challenge. Challenge submission form will require:
  - Screenshots of successully deploying the SDL on to a provider.
  - DSeqs for each of the deployment.
  - Deployer wallet address.
  - Timestamp of submission: The form submission timestamp will be used for this.
- **Timeline**: Participants will have ***6*** days to complete the task, in order to be eligible to receive reward, with rewards highest for those completing it on the first day of the week.
- **Incentive**: As detailed [here](https://docs.google.com/spreadsheets/d/1z_2Fx6u7U48LrxNj8IaDKjlnp84KOEgMb_hJw-Q1TjQ/edit#gid=2126550797).

### Task Type 5: Education Task (Intermediate)

- Participants who successfully complete any of the first four tasks types (Task Type 1 - Task Type 4) are encouraged to create an educational video of themselves doing the respective task type, for the benefit of others. Complete this task to be eligible for an additional reward.
- Video content must be in English.
- Video content must be uploaded to YouTube.
- Must be 720p quality or higher.
- Must demonstrate successful completion of the task (start to finish).
- The first 50 submissions that meet the above criteria will be rewarded. Video quality will be evaluated by the Akash Insider's group and the Overclock Core team, with ultimate discretion resting with the Overclock Labs core team.
- **Timeline**: This should be done before the end of the testnet, to be eligible for reward.
- **Incentive**: As detailed [here](https://docs.google.com/spreadsheets/d/1z_2Fx6u7U48LrxNj8IaDKjlnp84KOEgMb_hJw-Q1TjQ/edit#gid=2126550797).

### Task Type 6: Social Sharing Task (Beginner)

- Participants who successfully complete any of the other (1-4) task types are encouraged to share their work on Social media (Twitter). Completing this social sharing task will make them eligible for an additional reward.
- Content must be in English.
- Content must be shared on Twitter, and must tag @akashnet_.
- The first 50 submissions that meet the above criteria will be rewarded. Video quality will be evaluated by the Akash Insider's group and the Overclock Core team, with ultimate discretion resting with the Overclock Labs core team.
